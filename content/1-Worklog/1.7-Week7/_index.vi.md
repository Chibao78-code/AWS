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
| Thứ Hai | Hoàn thiện logic chia đều/tùy chỉnh/theo phần trăm.<br>Xử lý phần dư khi chia đều (phải có ai đó nhận thêm mấy đồng lẻ).<br>Chia theo phần trăm phải cộng đúng 100, thêm check cho việc này. | 29/06/2026 | 29/06/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://www.mongodb.com/docs/manual/data-modeling/> |
| Thứ Ba | Tính số dư dùng aggregation của MongoDB.<br>Cộng tổng đã trả vs còn nợ theo từng thành viên, rồi suy ra ai nợ ai.<br>Rút gọn gợi ý settlement để không phải tạo một giao dịch cho mỗi khoản chi. | 30/06/2026 | 30/06/2026 | <https://www.mongodb.com/docs/manual/aggregation/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Tạo settlement và trạng thái (pending/confirmed/rejected).<br>Chỉ người nợ được đánh dấu đã trả, chỉ người nhận được xác nhận.<br>Ghi log mỗi lần đổi trạng thái, tiện debug sau này. | 01/07/2026 | 01/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Thiết kế schema metadata biên lai (key, content type, người upload).<br>Không lưu file trực tiếp trong MongoDB, chỉ lưu reference.<br>Phác interface upload service, sẽ gắn S3 vào sau. | 02/07/2026 | 02/07/2026 | <https://000057.awsstudygroup.com/> <br> <https://000069.awsstudygroup.com/> |
| Thứ Sáu | Nối màn hình nhóm/khoản chi/số dư/settlement.<br>Chạy thử toàn bộ luồng bằng tay vài lần.<br>Phát hiện số dư tính toán và số hiển thị không khớp, đã sửa lại. | 03/07/2026 | 03/07/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Kết quả đạt được trong tuần 7:

* Triển khai nhiều phương thức chia tiền kèm validation đầu vào và làm tròn.
* Tính được số dư và gợi ý settlement từ dữ liệu khoản chi.
* Bổ sung cơ chế thay đổi trạng thái settlement có kiểm soát.
* Tách metadata biên lai khỏi vấn đề lưu file nhị phân.
* Hoàn thành phiên bản end-to-end đầu tiên của luồng chi tiêu chính trong Splitly.
