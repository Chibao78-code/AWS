---
title: "Các bài blogs đã đăng"
date: 2026-07-07
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Trong quá trình học và tìm hiểu kiến trúc AWS, tôi đã đọc tài liệu gốc, đối chiếu hai báo cáo tham khảo và biên soạn lại ba chủ đề thực tế: vận hành Kubernetes ở quy mô doanh nghiệp, phòng thủ ứng dụng trước DDoS và thiết kế môi trường phát triển phù hợp với Agentic AI. Nội dung dưới đây không chỉ tóm tắt dịch vụ AWS mà tập trung vào bài toán, cách các thành phần phối hợp, giá trị đạt được và điều tôi rút ra sau khi nghiên cứu.

Ba bài đã được chia sẻ trong cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Ngày của từng trang được lấy theo ngày xuất bản bài nguồn trên AWS Architecture Blog vì Facebook yêu cầu đăng nhập mới hiển thị ngày bài đăng; do đó các ngày này không sao chép từ hai dự án tham khảo.

### [Blog 1 - Tối ưu vận hành Kubernetes với Amazon EKS Auto Mode](3.1-Blog1/)

Blog 1 phân tích hành trình Generali Malaysia hiện đại hóa các ứng dụng bảo hiểm bằng microservices trên Amazon EKS. Trọng tâm là cách EKS Auto Mode giảm công việc quản lý node, bản vá Bottlerocket, add-on, load balancer, storage và mở rộng tài nguyên, nhưng vẫn yêu cầu đội vận hành thiết kế maintenance window, Pod Disruption Budget và Node Disruption Budget để tránh cập nhật hạ tầng gây gián đoạn dịch vụ.

Bài viết cũng mô tả kiến trúc bảo mật và quan sát đi kèm: GuardDuty tương quan tín hiệu tấn công, Inspector ưu tiên lỗ hổng của image đang chạy, Network Firewall kiểm soát lưu lượng đi ra, Secrets Manager quản lý bí mật tập trung, còn CloudWatch và Managed Grafana cung cấp dashboard theo namespace. Phần chi phí giải thích cách dùng tag, split cost allocation, Savings Plans và Graviton để liên kết mức tiêu thụ Kubernetes với từng dự án kinh doanh.

**Ngày bài nguồn AWS:** 23/03/2026

**Bài Facebook:** [Xem bài đăng](https://www.facebook.com/photo?fbid=1647830246522148)

### [Blog 2 - AWS WAF giúp Scale to Win chống DDoS như thế nào](3.2-Blog2/)

Blog 2 trình bày một kiến trúc phòng thủ nhiều lớp được Scale to Win xây dựng sau các đợt DDoS vượt hai triệu request mỗi giây. Lưu lượng được đưa qua Amazon CloudFront và AWS WAF để hấp thụ, phân loại và chặn request độc hại tại edge trước khi chúng tiêu thụ tài nguyên của Application Load Balancer và máy chủ ứng dụng.

Điểm quan trọng không chỉ là rate limiting. Bài viết giải thích cách khóa origin bằng managed prefix list và shared secret header, kết hợp heuristic với JA3/JA4 fingerprint, tách machine-to-machine traffic khỏi browser traffic, đặt hai ngưỡng tốc độ cho người dùng trình duyệt, dùng CAPTCHA cho vùng nghi ngờ và phát hiện token CAPTCHA bị tái sử dụng từ nhiều địa chỉ IP. Đây là ví dụ rõ về việc cân bằng khả năng chống tấn công với nhu cầu không chặn nhầm người dùng hợp lệ.

**Ngày bài nguồn AWS:** 14/07/2025

**Bài Facebook:** [Xem bài đăng](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2180420536056240/)

### [Blog 3 - Kiến trúc hệ thống hỗ trợ phát triển Agentic AI trên AWS](3.3-Blog3/)

Blog 3 giải thích vì sao tốc độ tạo mã của AI không tự động làm chu kỳ phát triển nhanh hơn. Nếu hệ thống phụ thuộc vào môi trường cloud tồn tại lâu, pipeline chậm, codebase kết dính và kiểm thử thủ công, agent vẫn phải chờ hàng phút hoặc hàng giờ để biết một thay đổi có đúng hay không. Giải pháp là coi vòng phản hồi nhanh, ranh giới rõ ràng và khả năng xác minh tự động là yêu cầu kiến trúc ngay từ đầu.

Bài viết đi sâu vào mô phỏng cục bộ bằng AWS SAM, container và DynamoDB Local; phát triển ngoại tuyến cho AWS Glue; kiểm thử hybrid bằng stack cloud nhỏ; preview environment tạo theo yêu cầu; OpenAPI và contract-first design; cấu trúc domain/application/infrastructure; project rules; unit, contract và smoke test; tài liệu máy có thể đọc; cùng các guardrail CI/CD và phê duyệt của con người đối với thay đổi rủi ro cao.

**Ngày bài nguồn AWS:** 26/03/2026

**Bài Facebook:** [Xem bài đăng](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2201707250594235/?rdid=Le865pC3R2JaAgDY#)
