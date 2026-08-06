---
title: "Nhật ký công việc tuần 7"
date: 2026-06-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Hoàn thiện luồng chia chi phí và tính số dư.
* Bổ sung theo dõi settlement và hỗ trợ biên lai.
* Tích hợp các màn hình nghiệp vụ chính với backend API.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Hoàn thiện quy tắc chia đều, chia tùy chỉnh và theo phần trăm, bao gồm làm tròn và kiểm tra tổng. | 29/06/2026 | 29/06/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://www.mongodb.com/docs/manual/data-modeling/> |
| Thứ Ba | Triển khai tổng hợp số dư, quan hệ người nợ/người nhận và gợi ý settlement. | 30/06/2026 | 30/06/2026 | <https://www.mongodb.com/docs/manual/aggregation/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Bổ sung tạo settlement, chuyển trạng thái và kiểm tra quyền xác nhận. | 01/07/2026 | 01/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Thiết kế metadata biên lai và lớp upload file để chuẩn bị tích hợp Amazon S3. | 02/07/2026 | 02/07/2026 | <https://000057.awsstudygroup.com/> <br> <https://000069.awsstudygroup.com/> |
| Thứ Sáu | Tích hợp màn hình nhóm, khoản chi, số dư và settlement; chạy các ca kiểm thử xuyên suốt. | 03/07/2026 | 03/07/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Kết quả đạt được trong tuần 7:

* Triển khai nhiều phương thức chia tiền kèm validation đầu vào và làm tròn.
* Tính được số dư và gợi ý settlement từ dữ liệu khoản chi.
* Bổ sung cơ chế thay đổi trạng thái settlement có kiểm soát.
* Tách metadata biên lai khỏi vấn đề lưu file nhị phân.
* Hoàn thành phiên bản end-to-end đầu tiên của luồng chi tiêu chính trong Splitly.
