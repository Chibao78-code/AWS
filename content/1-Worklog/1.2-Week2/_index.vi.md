---
title: "Nhật ký công việc tuần 2"
date: 2026-05-25
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Hiểu Amazon VPC và mối quan hệ giữa subnet, route và gateway.
* Phân biệt Security Group với Network ACL.
* Xây dựng và kiểm tra một môi trường mạng public/private nhỏ.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Nghiên cứu cách lập kế hoạch CIDR, Availability Zone và thiết kế public/private subnet. | 25/05/2026 | 25/05/2026 | <https://000003.awsstudygroup.com/> |
| Thứ Ba | Tạo VPC, subnet, route table và Internet Gateway; theo dõi đường đi của gói tin. | 26/05/2026 | 26/05/2026 | <https://000003.awsstudygroup.com/> |
| Thứ Tư | So sánh Security Group có trạng thái với NACL không trạng thái và kiểm thử các rule vào/ra. | 27/05/2026 | 27/05/2026 | <https://000003.awsstudygroup.com/> |
| Thứ Năm | Nghiên cứu NAT Gateway, Elastic IP, VPC Flow Logs và truy cập Internet từ private subnet. | 28/05/2026 | 28/05/2026 | <https://000003.awsstudygroup.com/> <br> <https://000074.awsstudygroup.com/> |
| Thứ Sáu | Khởi tạo EC2 thử nghiệm, kiểm tra route và kết nối, sau đó dọn tài nguyên bài lab. | 29/05/2026 | 29/05/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 2:

* Hiểu cách VPC, subnet, route table, Internet Gateway và NAT Gateway phối hợp.
* Phân biệt cơ chế kiểm soát mạng ở cấp instance và cấp subnet.
* Thực hành lần theo đường đi request trước khi thay đổi rule.
* Kiểm tra được kết nối EC2 cơ bản bên trong VPC.
* Nâng cao nhận thức về cô lập mạng và thiết kế quyền truy cập tối thiểu.
