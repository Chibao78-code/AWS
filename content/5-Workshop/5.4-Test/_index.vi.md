+++
title = "Test"
date = 2026-08-06
weight = 4
chapter = false
pre = "<b>5.4. </b>"
+++

# KIỂM THỬ HỆ THỐNG SPLITLY

Kiểm tra theo từng lớp giúp xác định nhanh lỗi nằm ở AWS, tiến trình backend, bản build frontend hay Nginx.

## 1. Kiểm tra hạ tầng và kết nối

- CloudFormation stack ở trạng thái `CREATE_COMPLETE`.
- EC2 đang `Running`, status checks đạt yêu cầu và Session Manager kết nối được.
- Security Group cho phép truy cập cổng 80 từ máy kiểm thử.

![Kiểm tra instance](/images/5-Workshop/Splitly/5.4-Test/17h1.png)

## 2. Kiểm tra backend

```bash
pm2 status
pm2 logs splitly-api --lines 50
sudo ss -lntp | grep 5000
curl -i http://127.0.0.1:5000/api/
```

`splitly-api` cần ở trạng thái `online` và cổng 5000 phải được lắng nghe. API có thể trả về `200`, `401` hoặc `404` tùy route; quan trọng là có phản hồi HTTP thay vì lỗi kết nối.

![Kiểm tra PM2](/images/5-Workshop/Splitly/5.4-Test/17h2.png)

## 3. Kiểm tra frontend và Nginx

```bash
test -f /opt/splitly/app/dist/index.html && echo "Build exists"
sudo nginx -t
sudo systemctl is-active nginx
curl -I http://127.0.0.1
```

Kết quả mong đợi là file `dist/index.html` tồn tại, cấu hình Nginx hợp lệ, dịch vụ `active` và yêu cầu HTTP trả về mã thành công.

![Kiểm tra frontend build](/images/5-Workshop/Splitly/5.4-Test/17h3.png)

![Kiểm tra Nginx](/images/5-Workshop/Splitly/5.4-Test/17h4.png)

## 4. Kiểm thử từ trình duyệt

Truy cập `http://<EC2_PUBLIC_IP>` và kiểm tra các luồng quan trọng:

1. Trang Splitly tải được và refresh ở route con không trả về 404.
2. Đăng ký/đăng nhập hoạt động; thông báo lỗi được hiển thị rõ khi dữ liệu không hợp lệ.
3. Tạo nhóm, thêm thành viên và ghi nhận khoản chi.
4. Kết quả chia tiền và số dư của từng thành viên được cập nhật đúng.
5. Tải ảnh hóa đơn lên và mở lại được qua luồng S3 đã cấu hình.
6. Nếu đã nhập thông tin tích hợp, kiểm tra email, Google Sign-In và VNPay Sandbox.

![Giao diện Splitly hoạt động](/images/5-Workshop/Splitly/5.4-Test/17h5.png)

## 5. Đối chiếu log và lỗi thường gặp

| Hiện tượng | Thành phần cần kiểm tra |
|---|---|
| Không mở được Public IP | Security Group cổng 80, Public IP, trạng thái Nginx |
| Trang mở được nhưng API lỗi | `pm2 logs`, cổng 5000, `VITE_API_URL`, cấu hình `/api/` của Nginx |
| Backend không kết nối database | `MONGODB_URI`, Atlas Network Access, DNS và log PM2 |
| Không tải được hóa đơn | tên bucket, Region, IAM role của EC2, bucket policy/CORS nếu có |
| Refresh route React bị 404 | dòng `try_files $uri $uri/ /index.html` trong Nginx |

Cuối cùng, mở CloudWatch để xác nhận log/metric được gửi về và không có chuỗi lỗi lặp lại. Không ghi giá trị secret vào ảnh chụp màn hình hoặc log báo cáo.
