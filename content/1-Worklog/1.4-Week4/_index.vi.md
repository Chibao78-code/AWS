---
title: "Nhật ký công việc tuần 4"
date: 2026-06-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Hoàn thành giai đoạn nghiên cứu trước dự án về storage, database, identity và monitoring trên AWS.
* So sánh lựa chọn dịch vụ cho web application có dữ liệu nghiệp vụ và file người dùng tải lên.
* Chuẩn bị danh sách vấn đề kiến trúc trước khi bắt đầu phát triển Splitly.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Đọc về S3 object, storage class, versioning, lifecycle rule.<br>Bật versioning trên bucket test, upload/ghi đè file để xem nó hoạt động.<br>Set lifecycle rule chuyển object cũ sang class rẻ hơn, chủ yếu để thực hành. | 08/06/2026 | 08/06/2026 | <https://000057.awsstudygroup.com/> <br> <https://000069.awsstudygroup.com/> |
| Thứ Ba | So sánh RDS, DynamoDB, MongoDB Atlas.<br>Nghiêng về MongoDB Atlas vì thấy mô hình dữ liệu linh hoạt hơn.<br>Chưa chắc 100%, có thể sẽ xem lại quyết định này sau. | 09/06/2026 | 09/06/2026 | <https://000005.awsstudygroup.com/> <br> <https://000060.awsstudygroup.com/> |
| Thứ Tư | Đọc về cách IAM đánh giá policy, least privilege.<br>Lần theo ví dụ: explicit deny luôn thắng, phần này giờ rõ rồi.<br>Xem qua KMS, cách secret có thể lưu thay cho file env thông thường. | 10/06/2026 | 10/06/2026 | <https://000044.awsstudygroup.com/> <br> <https://000033.awsstudygroup.com/> <br> <https://000096.awsstudygroup.com/> |
| Thứ Năm | Tìm hiểu CloudWatch, SNS, Budgets, tagging.<br>Set alarm cơ bản -> SNS gửi thông báo test, nhận được email.<br>Ghi ý tưởng đặt tên tag đơn giản (tên project + env). | 11/06/2026 | 11/06/2026 | <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> <br> <https://000013.awsstudygroup.com/> |
| Thứ Sáu | Gom hết những gì học trong tuần thành một checklist.<br>Frontend, backend, database, storage, bảo mật, giám sát, chi phí - mỗi dòng một ý.<br>Vẫn còn vài câu hỏi mở, sẽ giải quyết dần khi bắt đầu code. | 12/06/2026 | 12/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 4:

* Hiểu lý do file upload và dữ liệu nghiệp vụ cần các loại storage phù hợp với mẫu truy cập khác nhau.
* Biết kết hợp IAM role, bucket policy và Block Public Access thay vì nhúng credential.
* So sánh lựa chọn database và điểm đánh đổi trong vận hành.
* Liên kết monitoring, alerting, backup và budget control với hoạt động của ứng dụng.
* Hoàn tất giai đoạn nghiên cứu và sẵn sàng bắt đầu phát triển Splitly ngày 15/06/2026.
