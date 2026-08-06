---
title: "Nhật ký công việc tuần 10"
date: 2026-07-20
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Hoàn thiện quy tắc nghiệp vụ và ranh giới module backend của Splitly.
* Chuẩn bị hạ tầng có thể tái tạo và cấu hình triển khai.
* Xác định kiểm tra bảo mật và tiêu chí nghiệm thu trước khi đưa lên AWS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Rà soát quyền xác nhận settlement và bảo đảm chỉ đúng bên liên quan được xác nhận thanh toán. | 20/07/2026 | 20/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Ba | Tách notification preference và rà soát phụ thuộc giữa notification với các module nghiệp vụ. | 21/07/2026 | 21/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Bổ sung, kiểm thử giới hạn thành viên theo gói và chuẩn hóa phản hồi lỗi API. | 22/07/2026 | 22/07/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Thiết kế CloudFormation cho VPC, subnet, route, Security Group, EC2, IAM Role, S3 và monitoring. | 23/07/2026 | 23/07/2026 | <https://000037.awsstudygroup.com/> |
| Thứ Sáu | Chuẩn bị mẫu biến môi trường, kế hoạch Nginx/PM2, quyền truy cập MongoDB Atlas và tiêu chí nghiệm thu. | 24/07/2026 | 24/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000096.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 10:

* Tăng cường phân quyền cho thao tác settlement.
* Cải thiện khả năng bảo trì notification module và validation gói nhóm.
* Chuyển yêu cầu hạ tầng thành thiết kế CloudFormation có thể lặp lại.
* Xác định cấu hình server an toàn, không commit credential.
* Chuẩn bị tiêu chí kiểm tra cho hạ tầng, backend, frontend, proxy, database và storage biên lai.
