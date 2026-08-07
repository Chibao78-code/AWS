---
title: "Nhật ký công việc tuần 8"
date: 2026-07-06
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Mở rộng Splitly với thông báo, khiếu nại và các tích hợp tùy chọn.
* Cải thiện validation, phân quyền và tổ chức module.
* Kiểm thử ứng dụng trước khi thiết kế phương án triển khai AWS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Thiết kế notification preference và inbox.<br>Làm setting riêng cho từng user chọn loại sự kiện nào cần thông báo.<br>Giữ trạng thái đã đọc/chưa đọc thay vì chỉ bắn cảnh báo một lần rồi thôi. | 06/07/2026 | 06/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Ba | Thêm trạng thái thông báo (chưa đọc/đã đọc/lưu trữ).<br>Cân nhắc nhắc settlement nên đặt lịch hay để thủ công.<br>Chọn thủ công trước, dễ test hơn. | 07/07/2026 | 07/07/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Làm form + endpoint gửi khiếu nại.<br>Kiểm tra trường bắt buộc, không có gì phức tạp.<br>Chỉ admin nhóm xử lý được khiếu nại, ghi log mỗi lần đổi trạng thái. | 08/07/2026 | 08/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Rà lại cách xử lý App Password Gmail và key VNPay Sandbox.<br>Xác nhận không có biến `VITE_` nào làm lộ secret vào bundle trình duyệt.<br>Check lại `.gitignore` có che đúng file env chưa. | 09/07/2026 | 09/07/2026 | <https://support.google.com/accounts/answer/185833> <br> <https://sandbox.vnpayment.vn/apis/docs/> <br> <https://000096.awsstudygroup.com/> |
| Thứ Sáu | Test hồi quy thủ công toàn bộ module bằng một tài khoản test.<br>Liệt kê biến môi trường và cổng mà app cần dùng thật.<br>Ghi lại thành yêu cầu tiên quyết cho workshop deploy AWS sắp tới. | 10/07/2026 | 10/07/2026 | [../../5-workshop/](../../5-workshop/) <br> [../../2-proposal/](../../2-proposal/) |

### Kết quả đạt được trong tuần 8:

* Bổ sung mô hình notification và preference có cấu trúc.
* Hoàn thành luồng khiếu nại cơ bản giữa người dùng và quản trị viên.
* Cải thiện tách module, validation và kiểm tra quyền.
* Ghi nhận ranh giới an toàn cho thông tin xác thực của dịch vụ ngoài.
* Tạo phiên bản ứng dụng ổn định để bắt đầu thiết kế kiến trúc AWS.
