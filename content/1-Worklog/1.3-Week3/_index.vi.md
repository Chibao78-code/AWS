---
title: "Nhật ký công việc tuần 3"
date: 2026-06-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Tìm hiểu cách chọn EC2 instance, image, storage và phương thức truy cập.
* Hiểu mở rộng tài nguyên, cân bằng tải, tự động cấu hình và giám sát.
* Thực hành triển khai và chẩn đoán một web workload đơn giản.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | So sánh các họ EC2, hình thức mua, AMI và AWS Nitro System. Xem xét các họ general-purpose, compute-optimized và memory-optimized để phù hợp với từng loại workload, và so sánh hình thức On-Demand, Reserved, Spot để hiểu đánh đổi chi phí cho dự án quy mô sinh viên. | 01/06/2026 | 01/06/2026 | <https://000004.awsstudygroup.com/> |
| Thứ Ba | Nghiên cứu EBS volume, snapshot, instance store, key pair và truy cập bằng Session Manager. So sánh volume gp3 với các loại io theo nhu cầu throughput/IOPS, thực hành tạo snapshot để backup, và tìm hiểu vì sao Session Manager giúp tránh mở public key pair SSH ra Internet. | 02/06/2026 | 02/06/2026 | <https://000004.awsstudygroup.com/> <br> <https://000058.awsstudygroup.com/> |
| Thứ Tư | Khởi tạo EC2, gắn storage, sử dụng User Data và đọc instance metadata an toàn. Viết script User Data để tự động cài package khi khởi động, gắn thêm EBS volume và mount vào instance, và truy vấn metadata qua IMDSv2 thay vì IMDSv1 kém an toàn hơn. | 03/06/2026 | 03/06/2026 | <https://000004.awsstudygroup.com/> |
| Thứ Năm | Tìm hiểu Auto Scaling, Application Load Balancer, health check và cơ chế thay thế instance lỗi. Xem xét cách Auto Scaling group dùng target-tracking policy để tăng/giảm instance, cấu hình health check cho target group của Application Load Balancer, và theo dõi cách một instance không khỏe được thay thế tự động. | 04/06/2026 | 04/06/2026 | <https://000006.awsstudygroup.com/> |
| Thứ Sáu | Kiểm tra metric/log CloudWatch, chẩn đoán một lỗi thử nghiệm và dọn môi trường. Xem metric CPU và network của instance thử nghiệm, chủ động dừng dịch vụ web để quan sát trạng thái alarm CloudWatch tương ứng, sau đó terminate toàn bộ tài nguyên bài lab để tránh phát sinh phí. | 05/06/2026 | 05/06/2026 | <https://000008.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 3:

* Biết lựa chọn cấu hình EC2 và storage theo yêu cầu workload.
* Hiểu khác biệt giữa EBS bền vững và instance storage tạm thời.
* Thực hành tự động cấu hình và phương thức quản trị an toàn hơn.
* Hiểu vai trò của health check, load balancing và scaling.
* Biết sử dụng metric và log làm bằng chứng khi xử lý lỗi.
