---
title: "Blog 1"
date: 2026-06-04
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# TỐI ƯU VẬN HÀNH KUBERNETES VỚI AMAZON EKS AUTO MODE

**Ngày bài nguồn AWS:** 23/03/2026

**Chủ đề:** Kubernetes, vận hành, bảo mật, quan sát và tối ưu chi phí

Ngành bảo hiểm đang chuyển nhiều dịch vụ số lên đám mây để đáp ứng nhu cầu truy cập nhanh, ổn định và nhất quán của khách hàng. Generali Malaysia bắt đầu di chuyển lên AWS từ năm 2019 và chọn Amazon Elastic Kubernetes Service (Amazon EKS) làm nền tảng cho các ứng dụng được hiện đại hóa. Khi số lượng microservice và nhóm sử dụng tăng lên, vấn đề không còn là chạy được container mà là vận hành nhiều workload an toàn, đáng tin cậy và có chi phí kiểm soát được.

Bài viết này tổng hợp cách Generali kết hợp Amazon EKS Auto Mode với các dịch vụ bảo mật, quan sát và quản lý chi phí của AWS. Điểm quan trọng nhất là tự động hóa hạ tầng không đứng riêng lẻ: hệ thống chỉ bền vững khi quá trình cập nhật, bảo mật, giám sát và phân bổ chi phí được thiết kế đồng bộ.

## 1. Bài toán khi Kubernetes mở rộng

Trong một cluster thông thường, đội vận hành phải cấp phát và thay thế node, vá hệ điều hành, quản lý EKS add-on, cấu hình storage và load balancer, nâng cấp phiên bản Kubernetes, theo dõi tài nguyên và xử lý sự cố. Khi nhiều dự án cùng chia sẻ nền tảng, các tác vụ thủ công dễ tạo ra ba vấn đề:

* Cấu hình giữa các cluster hoặc tenant không nhất quán, từ đó làm tăng rủi ro bảo mật và tuân thủ.
* Tài nguyên thường bị cấp phát dư để phòng ngừa tải tăng, khiến chi phí cao nhưng hiệu suất sử dụng thấp.
* Kỹ sư dành nhiều thời gian bảo trì hạ tầng hơn là hỗ trợ nhóm phát triển và cải thiện sản phẩm.

Generali cần duy trì một đội vận hành gọn nhưng vẫn mở rộng số lượng ứng dụng. Vì vậy, họ áp dụng các nguyên tắc của AWS Well-Architected Framework, đặc biệt là Operational Excellence, Security, Reliability, Performance Efficiency và Cost Optimization.

## 2. Vai trò của Amazon EKS Auto Mode

EKS Auto Mode mở rộng phạm vi hạ tầng mà AWS quản lý cho cluster. Dịch vụ tự động xử lý các thành phần quan trọng sau:

* Chọn, cấp phát và thay thế EC2 node dựa trên nhu cầu thực tế của workload và cấu hình node pool.
* Tự động mở rộng hoặc thu hẹp tài nguyên, hạn chế việc duy trì node nhàn rỗi.
* Cung cấp khả năng tích hợp được quản lý cho load balancing và block storage.
* Vá Bottlerocket, cập nhật các EKS add-on mặc định và hỗ trợ nâng cấp cluster.
* Chuẩn hóa cách triển khai hạ tầng để các nhóm ứng dụng không phải tự xây một quy trình node riêng.

Nhờ đó, đội DevOps có thể chuyển trọng tâm từ công việc lặp lại sang kiểm soát chất lượng workload, khả năng tương thích khi nâng cấp và hỗ trợ nhóm ứng dụng. Tuy nhiên, “tự động” không có nghĩa là không cần thiết kế vận hành.

## 3. Kiểm soát gián đoạn khi node được cập nhật

EKS Auto Mode thường xuyên phát hành Amazon Machine Image mới và thay node cũ bằng node đã cập nhật. Nếu workload không được chuẩn bị, việc thay node có thể đồng thời dừng nhiều pod của một dịch vụ và gây gián đoạn.

Generali giảm rủi ro này bằng cách:

* Chọn maintenance window vào khung giờ thấp tải để các thay đổi ít ảnh hưởng đến người dùng.
* Cấu hình **Pod Disruption Budget** nhằm giữ lại số lượng pod tối thiểu của từng dịch vụ trong lúc bảo trì.
* Cấu hình **Node Disruption Budget** để giới hạn số node có thể bị thay thế cùng lúc.
* Dùng **Horizontal Pod Autoscaler** để số pod thay đổi theo lưu lượng thay vì cố định ở một mức quá lớn.
* Triển khai microservice stateless, xem pod là thành phần bất biến và dùng Helm chart làm cơ chế triển khai chuẩn.

Các nguyên tắc trên tách dữ liệu bền vững khỏi vòng đời pod. Khi một pod hoặc node bị thay thế, hệ thống có thể tạo bản sao mới mà không mất trạng thái quan trọng.

## 4. Kiến trúc bảo mật nhiều lớp

EKS Auto Mode giảm công việc quản lý hạ tầng nhưng không thay thế các lớp bảo mật. Generali bổ sung nhiều dịch vụ để phát hiện, ưu tiên và ngăn chặn mối đe dọa ở các điểm khác nhau.

### Amazon GuardDuty Extended Threat Detection

GuardDuty thu thập và tương quan tín hiệu từ EKS audit log, hành vi runtime, hoạt động malware và AWS API. Thay vì xem từng cảnh báo riêng lẻ, Extended Threat Detection có thể xây dựng chuỗi sự kiện của một cuộc tấn công nhiều giai đoạn, ví dụ từ khai thác container đến nâng quyền và di chuyển trong cluster.

Giá trị vận hành là đội bảo mật nhìn thấy tài nguyên bị ảnh hưởng, trình tự sự kiện và mức độ ưu tiên trong cùng một kết quả điều tra. Điều này rút ngắn thời gian phân tích và giúp tập trung xử lý vào phần có khả năng tạo blast radius lớn nhất.

### Amazon Inspector

Một image có lỗ hổng trong repository chưa chắc đang được sử dụng, trong khi một image đang chạy trên nhiều pod cần được xử lý sớm. Inspector ánh xạ image trong Amazon ECR với container đang chạy trên EKS, cung cấp cluster ARN, số pod sử dụng và thời điểm image được dùng gần nhất.

Nhờ ngữ cảnh runtime này, đội ngũ ưu tiên vá theo mức độ phơi nhiễm thực tế thay vì chỉ dựa trên danh sách CVE dài trong kho image.

### AWS Network Firewall

Workload bị xâm nhập thường cố kết nối ra ngoài để tải thêm mã độc hoặc gửi dữ liệu. Generali triển khai EKS trong private subnet và đưa lưu lượng đi ra qua Network Firewall. Chính sách có thể cho phép HTTPS đến danh sách hostname đã phê duyệt dựa trên Server Name Indication, đồng thời ghi lại hostname trong CloudWatch để phân tích.

Kiểm soát egress này giảm khả năng một container truy cập dịch vụ ngoài không được phép và tạo dữ liệu phục vụ kiểm toán, phát hiện hành vi bất thường.

### AWS Secrets Manager và External Secrets Operator

Secret không nên được ghi trực tiếp trong mã nguồn, Helm chart hoặc deployment manifest. Generali lưu credential tập trung trong Secrets Manager và dùng External Secrets Operator để đồng bộ giá trị cần thiết thành Kubernetes Secret theo chu kỳ.

Thiết kế này tách vòng đời credential khỏi mã ứng dụng, hỗ trợ rotation, ghi nhận truy cập và tránh buộc nhóm phát triển phải tự xây daemon hoặc logic lấy secret riêng.

## 5. Quan sát theo cluster, namespace và ứng dụng

Một nền tảng đa tenant cần cho từng nhóm thấy đúng metric và log của phần họ sở hữu. Generali dùng Amazon CloudWatch làm nguồn dữ liệu, thu thập chỉ số về cluster health, node, pod, mức sử dụng tài nguyên và ứng dụng. Amazon Managed Grafana trình bày các dữ liệu đó thành dashboard theo EKS namespace hoặc dự án.

Nhờ dashboard và cảnh báo có phạm vi rõ ràng, đội vận hành có thể nhanh chóng xác định sự cố thuộc node, cấu hình Kubernetes hay chính ứng dụng. Việc không phải tự quản lý hạ tầng Grafana cũng giảm thêm một lớp bảo trì.

## 6. Phân bổ và tối ưu chi phí

Tự động scale chỉ giải quyết một phần bài toán chi phí. Do nhiều đơn vị kinh doanh dùng chung nền tảng, Generali còn phải xác định dự án nào tạo ra mức tiêu thụ nào. AWS Billing split cost allocation data cho Amazon EKS sử dụng các tag như cluster, namespace, deployment và node để phân bổ chi phí Kubernetes cùng với phần chi tiêu AWS khác.

Từ dữ liệu đó, đội ngũ có thể:

* Phát hiện namespace hoặc deployment dùng tài nguyên vượt nhu cầu và thực hiện right-sizing.
* Áp dụng EC2 Savings Plans cho nhóm instance đã chọn trong node pool khi nhu cầu nền ổn định.
* Dùng instance Graviton có chi phí thấp hơn khi container image tương thích ARM64.
* Thảo luận chi phí dựa trên từng ứng dụng và đơn vị kinh doanh thay vì chỉ nhìn tổng hóa đơn của cluster.

## 7. Kết quả đạt được

Sự kết hợp giữa EKS Auto Mode và hệ sinh thái AWS giúp Generali chuyển từ môi trường Kubernetes nhiều tác vụ thủ công sang nền tảng có tính tự động hóa và tiêu chuẩn hóa cao hơn. Những giá trị chính gồm giảm khối lượng quản trị node và nâng cấp, cải thiện bảo mật nhờ phát hiện mối đe dọa và ưu tiên lỗ hổng, rút ngắn thời gian xác định nguyên nhân sự cố, tối ưu tài nguyên và tăng tốc độ đưa ứng dụng lên môi trường hoạt động.

Kết quả quan trọng hơn là đội DevOps có thêm thời gian hỗ trợ nhóm ứng dụng và chuẩn bị nền tảng cho các workload mới, bao gồm mô hình AI và ứng dụng agentic, thay vì liên tục xử lý công việc hạ tầng lặp lại.

## 8. Điều bản thân rút ra

Qua trường hợp này, tôi nhận thấy một nền tảng Kubernetes production không nên được đánh giá chỉ bằng việc cluster có chạy hay không. Cần xem đồng thời năm câu hỏi: hạ tầng có tự động cập nhật được không, cập nhật có làm gián đoạn workload không, mối đe dọa và lỗ hổng có được ưu tiên đúng không, mỗi nhóm có quan sát được phần mình phụ trách không, và chi phí có truy ngược về ứng dụng được không.

EKS Auto Mode giải quyết đáng kể phần compute và vòng đời cluster, nhưng hiệu quả thực sự đến từ việc kết hợp disruption budget, workload stateless, threat detection, vulnerability management, egress control, secret management, observability và cost allocation thành một kiến trúc thống nhất.

## Liên kết bài viết

* [Bài đăng trên Facebook](https://www.facebook.com/photo?fbid=1647830246522148)
* [Bài viết nguồn trên AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/how-generali-malaysia-optimizes-operations-with-amazon-eks/)
