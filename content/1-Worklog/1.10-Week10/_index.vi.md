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
| Thứ Hai | Kiểm tra lại quyền xác nhận settlement.<br>Đảm bảo một thành viên bất kỳ không xác nhận được settlement không phải của mình.<br>Thêm test case đúng chỗ này, nó pass nhưng vẫn muốn có bằng chứng rõ ràng. | 20/07/2026 | 20/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Ba | Tách logic notification preference ra service riêng.<br>Trước đó nó dính quá chặt với code khoản chi/settlement.<br>Lần theo xem sự kiện nào đang tạo notification, thấy thiếu vài chỗ. | 21/07/2026 | 21/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Tư | Thêm giới hạn 5 thành viên cho nhóm Free Plan.<br>Test thêm thành viên thứ 6, nhận đúng lỗi mong đợi.<br>Dọn lại format response lỗi, trước đó không đồng nhất giữa các endpoint. | 22/07/2026 | 22/07/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Viết CloudFormation template: VPC, subnet, route, SG, EC2, IAM Role, S3.<br>Thêm luôn tài nguyên alarm CloudWatch vào cùng template.<br>Gặp lỗi circular dependency một lần, sắp lại thứ tự resource mới hết. | 23/07/2026 | 23/07/2026 | <https://000037.awsstudygroup.com/> |
| Thứ Sáu | Soạn `.env.example` với toàn bộ biến backend EC2 cần dùng.<br>Lên kế hoạch cấu hình Nginx và tên process PM2 ra giấy trước.<br>Viết checklist ngắn xem "deploy xong" nghĩa là gì cụ thể. | 24/07/2026 | 24/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000096.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 10:

* Tăng cường phân quyền cho thao tác settlement.
* Cải thiện khả năng bảo trì notification module và validation gói nhóm.
* Chuyển yêu cầu hạ tầng thành thiết kế CloudFormation có thể lặp lại.
* Xác định cấu hình server an toàn, không commit credential.
* Chuẩn bị tiêu chí kiểm tra cho hạ tầng, backend, frontend, proxy, database và storage biên lai.
