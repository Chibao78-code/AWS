---
title: "Nhật ký công việc tuần 9"
date: 2026-07-13
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Thiết kế kiến trúc AWS phù hợp với quy mô và ngân sách hiện tại của Splitly.
* Xác định mạng, compute, lưu biên lai, kết nối database, giám sát và kiểm soát chi phí.
* Ghi nhận giới hạn hiện tại và lộ trình mở rộng thực tế.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Mô hình hóa luồng giữa trình duyệt, React/Vite, Nginx, Node.js/Express, MongoDB Atlas và dữ liệu biên lai. | 13/07/2026 | 13/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000112.awsstudygroup.com/> |
| Thứ Ba | Thiết kế VPC, public subnet, Internet Gateway, Security Group, EC2 và địa chỉ public ổn định. | 14/07/2026 | 14/07/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |
| Thứ Tư | Thiết kế S3 Receipts Bucket và IAM Role tối thiểu cho EC2; tách file khỏi metadata. | 15/07/2026 | 15/07/2026 | <https://000069.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| Thứ Năm | Bổ sung Session Manager, CloudWatch, SNS, AWS Budgets, hướng dẫn quản lý secret và tagging. | 16/07/2026 | 16/07/2026 | <https://000058.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Thứ Sáu | Hoàn thiện sơ đồ hiện tại và đề xuất mở rộng với CloudFront, Route 53, ACM, WAF, ALB và CI/CD. | 17/07/2026 | 17/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000094.awsstudygroup.com/> <br> <https://000026.awsstudygroup.com/> <br> <https://000017.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 9:

* Lựa chọn kiến trúc một EC2 phù hợp phạm vi dự án sinh viên hiện tại.
* Xác định luồng request xuyên suốt và các trust boundary.
* Không mở public cổng backend 5000 và lập phương án quản trị bằng Session Manager.
* Bổ sung yêu cầu quan sát, cảnh báo, ngân sách và quản lý secret.
* Ghi nhận hạn chế của single instance và lộ trình mở rộng theo nhu cầu thực tế.
