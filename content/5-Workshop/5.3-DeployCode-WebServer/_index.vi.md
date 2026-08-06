+++
title = "DeployCode-WebServer"
date = 2026-08-06
weight = 3
chapter = false
pre = "<b>5.3. </b>"
+++

# TRIỂN KHAI SPLITLY TRÊN EC2

## 1. Kết nối EC2 bằng Session Manager

Mở **EC2 → Instances**, chọn instance của Splitly, chọn **Connect → Session Manager → Connect**.

![Kết nối Session Manager](/images/5-Workshop/Splitly/5.3-Deploy-Config/12.png)

Chuyển sang người dùng ứng dụng, tạo thư mục triển khai và lấy mã nguồn:

```bash
sudo su - ec2-user
sudo mkdir -p /opt/splitly
sudo chown -R ec2-user:ec2-user /opt/splitly
cd /opt/splitly
git clone <URL_GITHUB_REPOSITORY> .
ls -la
```

Kết quả cần có hai thư mục chính:

```text
/opt/splitly/app
/opt/splitly/backend
```

Nếu repository riêng tư, hãy dùng cơ chế xác thực ngắn hạn hoặc deploy key có quyền đọc; không ghi token trực tiếp vào tài liệu hay lịch sử lệnh.

## 2. Cấu hình và chạy backend

Tạo file môi trường riêng cho backend:

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

Cài dependency, build và chạy API bằng PM2:

```bash
npm install
npm run build
pm2 start dist/server.js --name splitly-api
pm2 save
pm2 status
```

![Build và chạy backend](/images/5-Workshop/Splitly/5.3-Deploy-Config/13.png)

Tiến trình `splitly-api` phải ở trạng thái `online`. Khi cần chẩn đoán:

```bash
pm2 logs splitly-api --lines 100
sudo ss -lntp | grep 5000
```

## 3. Build frontend

Tạo cấu hình production cho React/Vite:

```bash
cd /opt/splitly/app
nano .env.production
```

```dotenv
VITE_API_URL=http://<EC2_PUBLIC_IP>
VITE_RECEIPTS_PUBLIC_BASE_URL=
VITE_GOOGLE_CLIENT_ID=<GOOGLE_CLIENT_ID>
```

Sau đó cài dependency và tạo bản build tĩnh:

```bash
npm install
npm run build
test -f dist/index.html && echo "Frontend build OK"
```

![Build frontend](/images/5-Workshop/Splitly/5.3-Deploy-Config/14.png)

Các biến bắt đầu bằng `VITE_` được đưa vào bundle phía trình duyệt, vì vậy không đặt password, secret hoặc access key trong file này.

## 4. Cấu hình Nginx

Tạo virtual host cho Splitly:

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

Kiểm tra cú pháp rồi khởi động lại dịch vụ:

```bash
sudo nginx -t
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl is-active nginx
```

![Cấu hình Nginx](/images/5-Workshop/Splitly/5.3-Deploy-Config/15.png)

![Khởi động Nginx](/images/5-Workshop/Splitly/5.3-Deploy-Config/16.png)

Nginx chỉ công khai cổng 80; API vẫn nghe trên localhost cổng 5000. Cấu hình này vừa phục vụ Single Page Application, vừa tránh mở trực tiếp backend ra Internet.
