+++
title = "DeployCode-WebServer"
date = 2026-08-06
weight = 3
chapter = false
pre = "<b>5.3. </b>"
+++

# DEPLOY SPLITLY ON EC2

## 1. Connect through Session Manager

Open **EC2 → Instances**, select the Splitly instance, then choose **Connect → Session Manager → Connect**.

![Connect with Session Manager](/images/5-Workshop/Splitly/5.3-Deploy-Config/12.png)

Prepare the deployment directory and clone the repository:

```bash
sudo su - ec2-user
sudo mkdir -p /opt/splitly
sudo chown -R ec2-user:ec2-user /opt/splitly
cd /opt/splitly
git clone <URL_GITHUB_REPOSITORY> .
ls -la
```

The repository should provide `/opt/splitly/app` and `/opt/splitly/backend`. For a private repository, use short-lived authentication or a read-only deploy key; never paste a token into the report.

## 2. Configure and run the backend

```bash
cd /opt/splitly/backend
nano .env
```

```dotenv
PORT=5000
MONGODB_URI=<MONGODB_ATLAS_CONNECTION_STRING>
MONGODB_DB=Splitly
JWT_SECRET=<RANDOM_LONG_SECRET>

EMAIL_PROVIDER=gmail
GMAIL_SMTP_USER=<GMAIL_ADDRESS>
GMAIL_APP_PASSWORD=<GMAIL_APP_PASSWORD>
EMAIL_FROM="Splitly <your-email@example.com>"

AWS_REGION=ap-southeast-1
S3_RECEIPTS_BUCKET=<S3_BUCKET_NAME>
S3_RECEIPTS_PREFIX=receipts/
S3_PRESIGN_EXPIRES_SECONDS=3000

FRONTEND_URL=http://<EC2_PUBLIC_IP>

VNPAY_TMN_CODE=
VNPAY_HASH_SECRET=
VNPAY_URL=https://sandbox.vnpayment.vn/paymentv2/vpcpay.html
```

Install, build, and start the API:

```bash
npm install
npm run build
pm2 start dist/server.js --name splitly-api
pm2 save
pm2 status
```

![Build and run backend](/images/5-Workshop/Splitly/5.3-Deploy-Config/13.png)

The process must be `online`. For diagnosis, use `pm2 logs splitly-api --lines 100` and `sudo ss -lntp | grep 5000`.

## 3. Build the frontend

```bash
cd /opt/splitly/app
nano .env.production
```

```dotenv
VITE_API_URL=http://<EC2_PUBLIC_IP>
VITE_RECEIPTS_PUBLIC_BASE_URL=
VITE_GOOGLE_CLIENT_ID=<GOOGLE_CLIENT_ID>
```

```bash
npm install
npm run build
test -f dist/index.html && echo "Frontend build OK"
```

![Build frontend](/images/5-Workshop/Splitly/5.3-Deploy-Config/14.png)

Every `VITE_` value is exposed to the browser bundle. Never put passwords, secrets, or AWS access keys in this file.

## 4. Configure Nginx

```bash
sudo nano /etc/nginx/conf.d/splitly.conf
```

```nginx
server {
    listen 80;
    server_name _;

    root /opt/splitly/app/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:5000;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

```bash
sudo nginx -t
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl is-active nginx
```

![Configure Nginx](/images/5-Workshop/Splitly/5.3-Deploy-Config/15.png)

![Start Nginx](/images/5-Workshop/Splitly/5.3-Deploy-Config/16.png)

Only port 80 is public. The API remains on localhost port 5000, while Nginx serves the Single Page Application and proxies API requests.
