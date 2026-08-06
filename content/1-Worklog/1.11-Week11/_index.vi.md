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
| Thứ Hai | Rà soát quyền triển khai, parameter, Region, tên tài nguyên, tính duy nhất của bucket và yêu cầu bảo vệ secret. | 27/07/2026 | 27/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000037.awsstudygroup.com/> |
| Thứ Ba | Tạo, theo dõi CloudFormation stack và kiểm tra VPC, subnet, route, Security Group, EC2, IAM Role cùng output. | 28/07/2026 | 28/07/2026 | <https://000037.awsstudygroup.com/> |
| Thứ Tư | Kết nối bằng Session Manager, clone repository, cấu hình backend, build API và chạy bằng PM2. | 29/07/2026 | 29/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://000058.awsstudygroup.com/> |
| Thứ Năm | Build frontend React/Vite và cấu hình Nginx phục vụ SPA, proxy `/api/` tới `127.0.0.1:5000`. | 30/07/2026 | 30/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Thứ Sáu | Kiểm tra kết nối MongoDB Atlas, quyền IAM của EC2 với S3 receipt bucket, trạng thái PM2, Nginx và dữ liệu CloudWatch ban đầu. | 31/07/2026 | 31/07/2026 | <https://www.mongodb.com/docs/atlas/> <br> <https://000048.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 11:

* Khởi tạo các tài nguyên mạng, compute, storage, identity và monitoring cần thiết.
* Quản trị EC2 qua Session Manager mà không cần mở SSH public.
* Chạy backend bằng PM2 và đặt cổng 5000 phía sau Nginx.
* Phục vụ production build React/Vite qua Nginx.
* Thiết lập luồng ứng dụng giữa EC2, MongoDB Atlas và S3 receipt bucket.
