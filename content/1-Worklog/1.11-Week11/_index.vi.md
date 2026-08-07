---
title: "Nhật ký công việc tuần 11"
date: 2026-07-27
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Khởi tạo hạ tầng thực hành Splitly trên AWS.
* Triển khai backend Node.js và frontend React/Vite trên Amazon EC2.
* Kết nối an toàn MongoDB Atlas, Amazon S3 và CloudWatch.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Kiểm tra lại quyền IAM trước khi deploy bất cứ thứ gì.<br>Xác nhận tên bucket S3 mình chọn thật sự chưa ai dùng.<br>Đảm bảo không có secret nào truyền vào dạng CloudFormation parameter thô. | 27/07/2026 | 27/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000037.awsstudygroup.com/> |
| Thứ Ba | Chạy `create-stack`, canh tab events xem có lỗi không.<br>Bị rollback một lần do gõ sai CIDR subnet, sửa lại rồi chạy lại.<br>Check output có đủ public IP của EC2 và tên bucket. | 28/07/2026 | 28/07/2026 | <https://000037.awsstudygroup.com/> |
| Thứ Tư | Mở session bằng Session Manager, clone repo vào instance.<br>Điền giá trị `.env` thật (MongoDB URI, JWT secret).<br>Build API, chạy bằng PM2, xem `pm2 logs` có lỗi gì không. | 29/07/2026 | 29/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://000058.awsstudygroup.com/> |
| Thứ Năm | Build frontend, copy file dist vào web root của Nginx.<br>Thêm fallback SPA để refresh route không bị 404.<br>Cấu hình proxy `/api/` trỏ về `127.0.0.1:5000`. | 30/07/2026 | 30/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Thứ Sáu | Xem log backend xác nhận kết nối MongoDB Atlas thành công.<br>Upload một biên lai test để chắc IAM Role thật sự hoạt động với S3.<br>`pm2 status` ổn, CloudWatch cũng đã bắt đầu có dữ liệu. | 31/07/2026 | 31/07/2026 | <https://www.mongodb.com/docs/atlas/> <br> <https://000048.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 11:

* Khởi tạo các tài nguyên mạng, compute, storage, identity và monitoring cần thiết.
* Quản trị EC2 qua Session Manager mà không cần mở SSH public.
* Chạy backend bằng PM2 và đặt cổng 5000 phía sau Nginx.
* Phục vụ production build React/Vite qua Nginx.
* Thiết lập luồng ứng dụng giữa EC2, MongoDB Atlas và S3 receipt bucket.
