---
title: "Nhật ký công việc tuần 6"
date: 2026-06-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Triển khai các module nghiệp vụ đầu tiên của Splitly.
* Kết nối frontend, REST API và MongoDB Atlas.
* Kiểm tra xác thực, thành viên nhóm và dữ liệu khoản chi.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Setup khung Express, kết nối DB.<br>Dùng một middleware xử lý lỗi chung thay vì try/catch lung tung.<br>App giờ báo lỗi ngay khi thiếu env var, tránh được một bug ngớ ngẩn. | 22/06/2026 | 22/06/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> <https://www.mongodb.com/docs/atlas/> |
| Thứ Ba | Làm đăng ký/đăng nhập, xác thực JWT.<br>Hash password, thêm thời hạn hết hiệu lực cho token.<br>Viết middleware chặn request thiếu/sai token, test bằng Postman. | 23/06/2026 | 23/06/2026 | <https://datatracker.ietf.org/doc/html/rfc7519> <br> <https://expressjs.com/en/guide/using-middleware.html> |
| Thứ Tư | Tạo nhóm và thêm thành viên.<br>Người tạo tự động thành admin.<br>Thêm kiểm tra chỉ admin sửa được cấu hình nhóm, quên bước này lúc đầu nên phải fix lại. | 24/06/2026 | 24/06/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Khoản chi: người trả, người tham gia, số tiền, danh mục, chia tiền.<br>Kiểm tra số tiền > 0 và người tham gia phải thuộc nhóm.<br>Thêm trường danh mục chủ yếu để lọc sau này, giờ chưa dùng tới. | 25/06/2026 | 25/06/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Sáu | Nối màn hình đăng nhập và nhóm với API.<br>Test case sai password, trùng tên nhóm.<br>Đối chiếu lại response API với dữ liệu thật trong MongoDB Atlas. | 26/06/2026 | 26/06/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Kết quả đạt được trong tuần 6:

* Xây dựng được luồng request từ React qua Express tới MongoDB Atlas.
* Hoàn thành cấu trúc xác thực và phân quyền ban đầu.
* Triển khai các thao tác cốt lõi cho nhóm, thành viên và khoản chi.
* Bổ sung validation để hạn chế thay đổi sai hoặc không đủ quyền.
* Thực hành chẩn đoán lỗi xuyên suốt frontend, backend và database.
