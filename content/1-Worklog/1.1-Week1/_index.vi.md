---
title: "Nhật ký công việc tuần 1"
date: 2026-05-18
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Làm quen với chương trình First Cloud AI Journey và quy trình học tập.
* Hiểu kiến thức điện toán đám mây cơ bản và hạ tầng toàn cầu của AWS.
* Tìm hiểu bảo mật tài khoản, IAM, AWS CLI và kiểm soát chi phí.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Tham gia chương trình, đọc lại yêu cầu thực tập.<br>Xem video hướng dẫn, ghi chú tiêu chí đánh giá.<br>Phác kế hoạch 12 tuần ra giấy trước, sau đó gõ lại thành file. | 18/05/2026 | 18/05/2026 | <https://youtu.be/AQlsd0nWdZk?si=QmmvhYeTisGPtctd> |
| Thứ Ba | Đọc về cloud, Region, AZ, edge location.<br>Ban đầu hơi lộn giữa Region và AZ, đọc lại tài liệu 2 lần mới rõ.<br>Ghi chú lại nhóm dịch vụ nào có khả năng cần dùng cho dự án sau này. | 19/05/2026 | 19/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Thứ Tư | Làm theo bước tạo tài khoản, bật MFA trên điện thoại.<br>Tạo IAM user thay vì dùng root, gắn policy cơ bản.<br>Thử cả inline policy và group policy để xem khác nhau chỗ nào. | 20/05/2026 | 20/05/2026 | <https://000001.awsstudygroup.com/> <br> <https://000002.awsstudygroup.com/> |
| Thứ Năm | Cài AWS CLI, chọn Region mặc định (ap-southeast-1).<br>Tạo named profile để không hardcode access key.<br>Chạy `aws sts get-caller-identity` kiểm tra, rồi thử liệt kê vài bucket. | 21/05/2026 | 21/05/2026 | <https://000011.awsstudygroup.com/> |
| Thứ Sáu | Đọc về Budgets, Cost Explorer, giới hạn Free Tier.<br>Set cảnh báo ngân sách ở ngưỡng nhỏ để test thử.<br>Kiểm tra Free Tier hiện tại vẫn còn xa mới tới giới hạn. | 22/05/2026 | 22/05/2026 | <https://000007.awsstudygroup.com/> <br> <https://000009.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 1:

* Hiểu hạ tầng toàn cầu AWS và vai trò của các nhóm dịch vụ compute, storage, networking, database và security.
* Làm quen với truy cập tài khoản an toàn bằng MFA và IAM identity thay cho root user.
* Cấu hình AWS CLI và thực hành các lệnh kiểm tra tài nguyên cơ bản.
* Biết thiết lập cảnh báo ngân sách và kiểm tra chi phí trước, sau mỗi bài lab.
* Hình thành thói quen ghi chép công việc và xóa tài nguyên không còn sử dụng.
