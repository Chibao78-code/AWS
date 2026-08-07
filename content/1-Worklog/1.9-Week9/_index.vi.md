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
| Thứ Hai | Vẽ luồng request: trình duyệt -> Nginx -> Express -> MongoDB Atlas.<br>Đánh dấu nơi file biên lai sẽ tách riêng khỏi dữ liệu nghiệp vụ.<br>Chưa code gì, tuần này chỉ vẽ sơ đồ. | 13/07/2026 | 13/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000112.awsstudygroup.com/> |
| Thứ Ba | Phác VPC + public subnet + IGW + Security Group + EC2.<br>Chọn 1 EC2 thôi, ngân sách không cho phép nhiều hơn.<br>Elastic IP để địa chỉ không đổi khi instance restart. | 14/07/2026 | 14/07/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |
| Thứ Tư | Lên kế hoạch S3 Receipts Bucket, bật Block Public Access.<br>IAM Role của EC2 chỉ giới hạn trong bucket đó, không rộng hơn.<br>DB chỉ lưu object key/URL, không lưu file thật. | 15/07/2026 | 15/07/2026 | <https://000069.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| Thứ Năm | Thêm Session Manager thay vì mở SSH ra public.<br>Liệt kê metric/alarm CloudWatch cần cho backend.<br>Ý tưởng tagging thô để sau này còn theo dõi chi phí được. | 16/07/2026 | 16/07/2026 | <https://000058.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Thứ Sáu | Hoàn tất sơ đồ cho giai đoạn này (1 EC2 duy nhất).<br>Viết ra list "để sau": CloudFront, Route 53, ACM, WAF, ALB, CI/CD.<br>Chưa làm gì trong số đó, chỉ ghi chú vào tài liệu proposal. | 17/07/2026 | 17/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000094.awsstudygroup.com/> <br> <https://000026.awsstudygroup.com/> <br> <https://000017.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 9:

* Lựa chọn kiến trúc một EC2 phù hợp phạm vi dự án sinh viên hiện tại.
* Xác định luồng request xuyên suốt và các trust boundary.
* Không mở public cổng backend 5000 và lập phương án quản trị bằng Session Manager.
* Bổ sung yêu cầu quan sát, cảnh báo, ngân sách và quản lý secret.
* Ghi nhận hạn chế của single instance và lộ trình mở rộng theo nhu cầu thực tế.
