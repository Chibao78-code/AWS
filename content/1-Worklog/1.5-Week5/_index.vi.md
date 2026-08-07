---
title: "Nhật ký công việc tuần 5"
date: 2026-06-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Bắt đầu dự án Splitly và xác định phạm vi phát triển đầu tiên.
* Phân tích người dùng, quy trình chi tiêu nhóm, quy tắc chia tiền và quan hệ dữ liệu.
* Xây dựng nền móng frontend, backend, database và quy trình Git.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Viết ra bài toán chi tiêu chung theo cách hiểu của mình.<br>Phác vai trò thành viên/admin, cố ý giữ list chức năng nhỏ.<br>Không muốn ôm quá nhiều việc ngay tuần đầu dự án. | 15/06/2026 | 15/06/2026 | [../../2-proposal/](../../2-proposal/) |
| Thứ Ba | Phác use case: đăng ký, nhóm, thành viên, khoản chi, số dư, settlement, biên lai, thông báo.<br>Vẽ nháp sequence diagram cho luồng đăng ký -> settlement.<br>Vài case biên (nhóm rỗng, 1 thành viên) tạm để TODO xử lý sau. | 16/06/2026 | 16/06/2026 | [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Setup folder cho frontend (React/Vite/TS) và backend (Node/Express/TS).<br>Bật strict mode trong tsconfig, sửa hết lỗi nó báo.<br>Test proxy dev của Vite với một route Express giả, chạy được. | 17/06/2026 | 17/06/2026 | <https://react.dev/learn> <br> <https://vite.dev/guide/> <br> <https://expressjs.com/en/guide/routing.html> <br> <https://www.mongodb.com/docs/atlas/> |
| Thứ Năm | Phác schema MongoDB đầu tiên: user, group, expense, settlement.<br>Đắn đo giữa embed và reference cho thành viên nhóm, chọn reference.<br>Thêm index cho trường thành viên nhóm vì sẽ query nhiều. | 18/06/2026 | 18/06/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Sáu | Đặt quy ước tên branch, đơn giản thôi không cầu kỳ.<br>Tạo `.env.example` với giá trị giả, thêm dòng vào `.gitignore`.<br>Chia kế hoạch 12 tuần thành mục tiêu code từng tuần, còn khá thô. | 19/06/2026 | 19/06/2026 | <https://git-scm.com/docs> <br> [../../2-proposal/](../../2-proposal/) |

### Kết quả đạt được trong tuần 5:

* Bắt đầu phát triển Splitly ngày 15/06/2026 với bài toán và phạm vi rõ ràng.
* Xác định người dùng, luồng nghiệp vụ và tiêu chí nghiệm thu chính.
* Lựa chọn stack React, Express, TypeScript và MongoDB Atlas phù hợp.
* Chuẩn bị mô hình dữ liệu và cấu trúc dự án ban đầu.
* Thống nhất nguyên tắc branch, review, biến môi trường và bảo vệ secret.
