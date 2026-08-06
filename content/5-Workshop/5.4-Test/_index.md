+++
title = "Test"
date = 2026-07-16
weight = 4
chapter = false
pre = "<b>5.4. </b>"
+++

# TEST THE SPLITLY DEPLOYMENT

Validate one layer at a time so failures can be assigned to AWS infrastructure, the API process, the frontend build, or Nginx.

## 1. Infrastructure and connectivity

- The stack is `CREATE_COMPLETE`.
- EC2 is `Running`, passes its status checks, and accepts a Session Manager connection.
- The Security Group permits HTTP port 80 from the test client.

![Check instance](/images/5-Workshop/Splitly/5.4-Test/17h1.png)

## 2. Backend

```bash
pm2 status
pm2 logs splitly-api --lines 50
sudo ss -lntp | grep 5000
curl -i http://127.0.0.1:5000/api/
```

`splitly-api` should be `online`, and port 5000 should be listening. Depending on the route, an HTTP response may be `200`, `401`, or `404`; a response is still different from a connection failure.

![Check PM2](/images/5-Workshop/Splitly/5.4-Test/17h2.png)

## 3. Frontend and Nginx

```bash
test -f /opt/splitly/app/dist/index.html && echo "Build exists"
sudo nginx -t
sudo systemctl is-active nginx
curl -I http://127.0.0.1
```

The build file must exist, Nginx syntax must pass, the service must be `active`, and the local HTTP request should return a successful response.

![Check frontend build](/images/5-Workshop/Splitly/5.4-Test/17h3.png)

![Check Nginx](/images/5-Workshop/Splitly/5.4-Test/17h4.png)

## 4. Browser and functional tests

Open `http://<EC2_PUBLIC_IP>` and verify:

1. Splitly loads and refreshing a client-side route does not return 404.
2. Registration and sign-in work, including clear validation failures.
3. A group, members, and expenses can be created.
4. Per-member balances and settlement results are updated correctly.
5. A receipt can be uploaded and retrieved through the configured S3 flow.
6. Email, Google Sign-In, and VNPay Sandbox work when their credentials were supplied.

![Splitly UI running](/images/5-Workshop/Splitly/5.4-Test/17h5.png)

## 5. Troubleshooting matrix

| Symptom | Check |
|---|---|
| Public IP does not open | Port 80 Security Group rule, public IP, Nginx status |
| UI loads but API fails | PM2 logs, port 5000, `VITE_API_URL`, Nginx `/api/` proxy |
| Database connection fails | `MONGODB_URI`, Atlas Network Access, DNS, PM2 logs |
| Receipt upload fails | Bucket name, Region, EC2 IAM role, bucket CORS/policy when applicable |
| React route refresh returns 404 | Nginx `try_files $uri $uri/ /index.html` |

Finally, verify that expected logs or metrics reach CloudWatch and that no repeated error pattern remains. Do not include secret values in screenshots or report logs.
