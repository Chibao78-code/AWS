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
| Thứ Hai | Xây dựng nền móng backend, kết nối database, xử lý lỗi chung và kiểm tra biến môi trường. | 22/06/2026 | 22/06/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> <https://www.mongodb.com/docs/atlas/> |
| Thứ Ba | Triển khai đăng ký, đăng nhập, xác thực bằng JWT và middleware bảo vệ route. | 23/06/2026 | 23/06/2026 | <https://datatracker.ietf.org/doc/html/rfc7519> <br> <https://expressjs.com/en/guide/using-middleware.html> |
| Thứ Tư | Phát triển chức năng tạo nhóm, thành viên, vai trò cơ bản và kiểm tra quyền chỉnh sửa. | 24/06/2026 | 24/06/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Triển khai khoản chi gồm người trả, người tham gia, số tiền, danh mục và thông tin chia tiền. | 25/06/2026 | 25/06/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Sáu | Kết nối các màn hình frontend đầu tiên với API, kiểm thử lỗi thường gặp và rà soát tính nhất quán dữ liệu. | 26/06/2026 | 26/06/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Kết quả đạt được trong tuần 6:

* Xây dựng được luồng request từ React qua Express tới MongoDB Atlas.
* Hoàn thành cấu trúc xác thực và phân quyền ban đầu.
* Triển khai các thao tác cốt lõi cho nhóm, thành viên và khoản chi.
* Bổ sung validation để hạn chế thay đổi sai hoặc không đủ quyền.
* Thực hành chẩn đoán lỗi xuyên suốt frontend, backend và database.
