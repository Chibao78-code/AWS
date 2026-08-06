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
| Thứ Hai | Thiết kế tùy chọn thông báo và inbox cho hoạt động nhóm, khoản chi và settlement. | 06/07/2026 | 06/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Ba | Bổ sung xử lý trạng thái thông báo và xem xét nhắc settlement định kỳ hoặc theo yêu cầu. | 07/07/2026 | 07/07/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Phát triển luồng gửi khiếu nại và xử lý của quản trị viên kèm kiểm tra dữ liệu, quyền truy cập. | 08/07/2026 | 08/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Rà soát ranh giới cấu hình Gmail/VNPay Sandbox và ngăn secret đi vào client code hoặc Git. | 09/07/2026 | 09/07/2026 | <https://support.google.com/accounts/answer/185833> <br> <https://sandbox.vnpayment.vn/apis/docs/> <br> <https://000096.awsstudygroup.com/> |
| Thứ Sáu | Kiểm thử xác thực, nhóm, khoản chi, settlement, thông báo và khiếu nại; ghi nhận yêu cầu triển khai. | 10/07/2026 | 10/07/2026 | [../../5-workshop/](../../5-workshop/) <br> [../../2-proposal/](../../2-proposal/) |

### Kết quả đạt được trong tuần 8:

* Bổ sung mô hình notification và preference có cấu trúc.
* Hoàn thành luồng khiếu nại cơ bản giữa người dùng và quản trị viên.
* Cải thiện tách module, validation và kiểm tra quyền.
* Ghi nhận ranh giới an toàn cho thông tin xác thực của dịch vụ ngoài.
* Tạo phiên bản ứng dụng ổn định để bắt đầu thiết kế kiến trúc AWS.
