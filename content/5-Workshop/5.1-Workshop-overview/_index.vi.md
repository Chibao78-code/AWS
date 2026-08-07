+++
title = "Giới thiệu"
date = 2026-08-06
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

# TỔNG QUAN WORKSHOP SPLITLY

## Bài toán

Khi đi du lịch, ở chung hoặc tổ chức hoạt động theo nhóm, nhiều thành viên có thể thanh toán thay nhau. Việc ghi chép thủ công dễ dẫn đến bỏ sót khoản chi, khó đối chiếu hóa đơn và mất thời gian tính xem ai cần hoàn tiền cho ai. Splitly tập trung danh sách thành viên, khoản chi, tỷ lệ chia và chứng từ vào một hệ thống thống nhất để số dư được cập nhật minh bạch.

## Kiến trúc được triển khai trong workshop

![Kiến trúc triển khai Splitly](/images/5-Workshop/Splitly/5.1-Overview/diagram1.png)

Luồng chính của hệ thống:

1. Người dùng truy cập địa chỉ public của EC2 qua HTTP cổng 80.
2. **Nginx** trả về các tệp đã build của React/Vite. Yêu cầu bắt đầu bằng `/api/` được chuyển tiếp đến backend ở `127.0.0.1:5000`.
3. **Node.js/Express** xử lý xác thực, nhóm, thành viên, khoản chi và logic chia tiền; tiến trình được quản lý bằng **PM2**.
4. Backend đọc/ghi dữ liệu nghiệp vụ trên **MongoDB Atlas** và lưu ảnh hóa đơn vào **Amazon S3** bằng quyền từ IAM role của EC2.
5. **Amazon CloudWatch** tiếp nhận log/metric phục vụ theo dõi và chẩn đoán. Quản trị viên kết nối máy chủ qua **AWS Systems Manager Session Manager**, nhờ đó không cần mở SSH công khai.

Trong phiên bản thực hành, frontend và backend cùng nằm trên một EC2 để dễ triển khai và kiểm chứng. Khi mở rộng sản phẩm, frontend có thể chuyển sang S3 + CloudFront, bổ sung Route 53, ACM và AWS WAF; đó là hướng phát triển tiếp theo, không phải tài nguyên bắt buộc của workshop hiện tại.

## Kết quả mong đợi

Cuối workshop, EC2 phải phục vụ được giao diện Splitly, API hoạt động qua Nginx, tiến trình `splitly-api` ở trạng thái `online`, dữ liệu kết nối được tới MongoDB Atlas và thao tác tải hóa đơn có thể sử dụng S3. Các bước kiểm thử được tách riêng để có thể xác định lỗi thuộc hạ tầng, backend, frontend hay web server.
