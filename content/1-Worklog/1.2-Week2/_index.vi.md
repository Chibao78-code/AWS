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
| Thứ Hai | Đọc về cách chia CIDR, Availability Zone.<br>Phác layout subnet ra giấy, một khối public, một khối private.<br>Cố giữ số liệu đơn giản, không tính toán quá phức tạp. | 25/05/2026 | 25/05/2026 | <https://000003.awsstudygroup.com/> |
| Thứ Ba | Tạo VPC, subnet, route table, IGW.<br>Gắn IGW vào VPC, set route mặc định cho public subnet.<br>Vẽ lại đường đi gói tin ra giấy để kiểm tra route có hợp lý không. | 26/05/2026 | 26/05/2026 | <https://000003.awsstudygroup.com/> |
| Thứ Tư | So sánh Security Group với NACL, thử vài rule.<br>SG dễ hơn vì có trạng thái, traffic trả về tự động được cho qua.<br>NACL phải khai rõ cả hai chiều, làm sai vài lần mới đúng. | 27/05/2026 | 27/05/2026 | <https://000003.awsstudygroup.com/> |
| Thứ Năm | Đọc về NAT Gateway, Elastic IP, Flow Logs.<br>Tạo NAT Gateway trong public subnet, gắn EIP vào.<br>Sửa route table của private subnet, bật Flow Logs để xem traffic. | 28/05/2026 | 28/05/2026 | <https://000003.awsstudygroup.com/> <br> <https://000074.awsstudygroup.com/> |
| Thứ Sáu | Khởi tạo EC2 test trong private subnet.<br>Xác nhận ra Internet được qua NAT nhưng không ai truy cập trực tiếp vào được.<br>Terminate ngay sau đó, xóa cả NAT Gateway và EIP, sợ để quên bị tính phí. | 29/05/2026 | 29/05/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 2:

* Hiểu cách VPC, subnet, route table, Internet Gateway và NAT Gateway phối hợp.
* Phân biệt cơ chế kiểm soát mạng ở cấp instance và cấp subnet.
* Thực hành lần theo đường đi request trước khi thay đổi rule.
* Kiểm tra được kết nối EC2 cơ bản bên trong VPC.
* Nâng cao nhận thức về cô lập mạng và thiết kế quyền truy cập tối thiểu.
