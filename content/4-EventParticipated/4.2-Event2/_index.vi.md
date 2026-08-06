---
title: "Event 2"
date: 2026-08-06
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# BÀI THU HOẠCH AWS, DEVOPS, AI VÀ SECURITY MEETUP

## 1. Tổng quan sự kiện

Event 2 là buổi meetup có phạm vi khá rộng, kết nối năm góc nhìn đang được quan tâm trong ngành công nghệ: hệ thống thời gian thực trên AWS, container hóa với Docker, GraphRAG, phát hiện xâm nhập bằng Machine Learning và lộ trình nghề nghiệp từ IT Helpdesk đến Cloud/DevOps.

Mặc dù mỗi phiên sử dụng một nhóm công nghệ khác nhau, thông điệp chung của sự kiện là không nên lựa chọn công cụ chỉ vì xu hướng. Kiến trúc phải xuất phát từ yêu cầu về độ trễ, khả năng mở rộng, độ tin cậy, bảo mật và năng lực vận hành của đội ngũ.

## 2. Mục tiêu của sự kiện

- Chia sẻ cách các dịch vụ AWS được sử dụng trong dự án thực tế.
- Làm rõ vai trò của Docker trong quá trình phát triển và triển khai phần mềm.
- Giới thiệu hướng kết hợp Generative AI với cơ sở dữ liệu đồ thị.
- Trình bày cách Machine Learning bổ sung cho hệ thống phòng thủ mạng dựa trên luật.
- Cung cấp góc nhìn thực tế về nghề System Administration, Cloud và DevOps.
- Tạo cơ hội để sinh viên học hỏi từ diễn giả và cộng đồng công nghệ.

## 3. Diễn giả

- **Nguyễn Quốc Bảo**
- **Huỳnh Quốc Bảo**
- **Việt Phát**
- **Lê Hoàng Gia Đại**
- **Trần Trung Vinh**

## 4. Nội dung nổi bật

### 4.1 Multiplayer in the Cloud – kết nối Godot Client với AWS WebSocket

Anh Nguyễn Quốc Bảo trình bày bài toán giao tiếp thời gian thực trong game multiplayer. Các phương án UDP, WebSocket và HTTP Polling được so sánh dựa trên cách duy trì kết nối, độ trễ và độ phức tạp triển khai.

WebSocket phù hợp khi client và server cần trao đổi hai chiều liên tục mà không phải tạo một HTTP request mới cho mỗi cập nhật. Trong mô hình được giới thiệu, client Godot kết nối tới hạ tầng AWS; Lambda xử lý logic theo sự kiện và DynamoDB lưu trạng thái cần thiết cho matchmaking hoặc phiên chơi. AWS GameLift được nhắc đến như một lựa chọn chuyên biệt hơn cho game session quy mô lớn.

Điểm rút ra là “thời gian thực” không chỉ phụ thuộc vào một giao thức. Hệ thống còn phải quản lý vòng đời kết nối, định danh người chơi, trạng thái bị ngắt, khả năng gửi lại dữ liệu và sự nhất quán giữa nhiều client.

### 4.2 Docker và tư duy container hóa

Anh Huỳnh Quốc Bảo giải thích sự khác biệt giữa máy ảo và container. Máy ảo cung cấp mức cô lập bằng cách chạy hệ điều hành khách, trong khi container chia sẻ kernel của máy chủ và đóng gói ứng dụng cùng dependency cần thiết. Nhờ đó, container thường khởi động nhanh hơn và sử dụng tài nguyên nhẹ hơn.

Docker giúp tạo một môi trường có thể lặp lại từ máy phát triển đến máy chủ. Image mô tả cách đóng gói, còn container là một phiên bản đang chạy của image đó. Giá trị thực tế nằm ở việc giảm tình trạng “chạy được trên máy của tôi”, chuẩn hóa quá trình build và tạo nền tảng cho CI/CD hoặc kiến trúc microservices.

Tuy nhiên, container không tự động giải quyết mọi vấn đề vận hành. Nhóm vẫn cần quản lý secret, storage, log, network, image vulnerability và quy trình cập nhật phiên bản.

### 4.3 Xây dựng GraphRAG với Amazon Bedrock và Amazon Neptune

Anh Việt Phát giới thiệu Retrieval-Augmented Generation (RAG) và giới hạn của việc chỉ tìm kiếm các đoạn văn độc lập. Với câu hỏi cần suy luận qua nhiều mối quan hệ, kết quả truy xuất theo độ tương đồng có thể thiếu ngữ cảnh liên kết.

GraphRAG bổ sung Knowledge Graph để biểu diễn thực thể và quan hệ. Amazon Neptune quản lý dữ liệu đồ thị, trong khi Amazon Bedrock cung cấp mô hình nền tảng phục vụ quá trình sinh câu trả lời. Cách tiếp cận này hỗ trợ truy vấn nhiều bước và giúp hệ thống giải thích được chuỗi quan hệ đã sử dụng.

Phiên chia sẻ cũng nhấn mạnh sự đánh đổi giữa managed service và giải pháp open-source. Dịch vụ được quản lý giảm công sức vận hành nhưng cần đánh giá chi phí, khả năng tùy chỉnh, quyền kiểm soát dữ liệu và mức độ phụ thuộc nhà cung cấp.

### 4.4 Machine Learning-based NIDS trên AWS

Anh Lê Hoàng Gia Đại trình bày mô hình kết hợp AWS WAF với Network Intrusion Detection System sử dụng Machine Learning. WAF hoạt động tốt với các rule đã biết, nhưng phương pháp chỉ dựa trên luật có thể khó nhận diện hành vi mới hoặc chuỗi tín hiệu phức tạp.

Dự án sử dụng bộ dữ liệu CSE-CIC-IDS2018 để huấn luyện mô hình phân loại lưu lượng và hiển thị kết quả qua dashboard thời gian thực. Machine Learning được dùng như một lớp phát hiện bổ sung nhằm nhận diện mẫu bất thường, trong khi WAF vẫn đảm nhiệm lọc request dựa trên rule.

Bài học quan trọng là mô hình ML không thay thế hoàn toàn kiểm soát bảo mật truyền thống. Hiệu quả phụ thuộc chất lượng dữ liệu, cách chọn đặc trưng, tỷ lệ false positive, khả năng cập nhật mô hình và quy trình con người xác minh cảnh báo.

### 4.5 Từ IT Helpdesk đến Senior System Administrator

Anh Trần Trung Vinh chia sẻ lộ trình phát triển từ IT Helpdesk sang System Administrator và định hướng Cloud/DevOps. Công việc Helpdesk tạo nền tảng về giao tiếp với người dùng, thu thập thông tin, phân loại lỗi và xử lý sự cố có hệ thống.

Để tiến lên vị trí Sysadmin, kiến thức Linux, networking, quyền truy cập, dịch vụ hệ thống và tự động hóa là những năng lực cốt lõi. Khi chuyển sang Cloud/DevOps, các kiến thức nền này vẫn giữ nguyên giá trị; dịch vụ cloud thay đổi cách cung cấp tài nguyên nhưng không loại bỏ nhu cầu hiểu hệ điều hành và mạng.

Phần chia sẻ về phỏng vấn và phát triển nghề nghiệp nhấn mạnh việc xây dựng lộ trình từng bước, thực hành qua project và có khả năng giải thích quyết định kỹ thuật thay vì chỉ ghi nhớ tên công cụ.

## 5. Những gì học được

### 5.1 Kiến thức kỹ thuật

- Biết các yếu tố cần cân nhắc khi chọn UDP, WebSocket hoặc HTTP Polling cho hệ thống thời gian thực.
- Hiểu container khác máy ảo như thế nào và Docker hỗ trợ tính nhất quán trong triển khai ra sao.
- Hiểu vì sao Knowledge Graph có thể cải thiện bài toán RAG cần suy luận nhiều bước.
- Nhận biết vai trò bổ trợ giữa AWS WAF, NIDS và Machine Learning trong mô hình phòng thủ nhiều lớp.
- Thấy được Linux, networking và kỹ năng xử lý sự cố là nền tảng chung của Sysadmin, Cloud và DevOps.

### 5.2 Tư duy kiến trúc và nghề nghiệp

- Chọn dịch vụ theo yêu cầu, không theo mức độ phổ biến.
- Đánh giá cả chi phí vận hành và độ phức tạp trước khi dùng managed service.
- Xem observability, security và deployment là một phần của thiết kế ngay từ đầu.
- Học qua dự án thực tế và ghi lại cách giải quyết vấn đề thay vì chỉ học lý thuyết.
- Xây dựng lộ trình nghề nghiệp từ kiến thức nền đến công cụ chuyên sâu.

## 6. Áp dụng vào dự án Splitly

Các ý tưởng của event có thể được chọn lọc cho Splitly như sau:

1. **Thông báo thời gian thực:** WebSocket có thể được cân nhắc trong tương lai cho thông báo nhóm hoặc trạng thái settlement. Ở quy mô hiện tại, REST API vẫn đơn giản và phù hợp hơn; chỉ thêm WebSocket khi có yêu cầu cập nhật tức thời rõ ràng.
2. **Container hóa:** đóng gói backend Node.js bằng Docker sẽ giúp môi trường build nhất quán và thuận lợi cho CI/CD. Đây là bước nâng cấp sau khi quy trình EC2 + PM2 hiện tại đã ổn định.
3. **AI có mục đích:** GraphRAG không cần thiết cho chức năng chia tiền cốt lõi. Nếu Splitly phát triển trợ lý truy vấn lịch sử chi tiêu hoặc mối quan hệ giao dịch phức tạp, nhóm mới nên đánh giá Bedrock/Neptune dựa trên giá trị và chi phí thực tế.
4. **Bảo mật nhiều lớp:** kiến trúc tương lai của Splitly có AWS WAF, nhưng vẫn cần Security Group tối thiểu, log CloudWatch, cập nhật dependency và quy trình phản hồi sự cố. ML-based NIDS chỉ phù hợp khi hệ thống có đủ lưu lượng và dữ liệu để huấn luyện/đánh giá.
5. **Nền tảng vận hành:** kiến thức Linux, networking và troubleshooting hỗ trợ trực tiếp việc cấu hình Nginx, PM2, port, DNS, IAM và chẩn đoán kết nối MongoDB/S3.
6. **Chuẩn hóa triển khai:** các bài học Docker và DevOps khuyến khích nhóm đưa build, kiểm thử và cấu hình hạ tầng vào quy trình có thể lặp lại thay vì thao tác thủ công không được ghi chép.

## 7. Trải nghiệm và cảm nhận

Điểm mình đánh giá cao là sự kiện trình bày công nghệ thông qua các bài toán cụ thể: multiplayer cần kết nối liên tục, Docker giải quyết sự khác biệt môi trường, GraphRAG xử lý quan hệ dữ liệu, NIDS tìm dấu hiệu tấn công và Sysadmin chịu trách nhiệm duy trì hệ thống. Nhờ đó, các dịch vụ AWS không còn là danh sách tên gọi riêng lẻ mà trở thành công cụ trong một quyết định kiến trúc.

![Hình ảnh tại sự kiện](/images/4-Event/Splitly/event-2-meetup-2026.jpg)

> Sau sự kiện, mình hiểu rõ hơn rằng phát triển Cloud/DevOps cần cả chiều rộng lẫn chiều sâu: biết nhiều hướng công nghệ để lựa chọn, nhưng vẫn phải nắm chắc Linux, networking, bảo mật và khả năng vận hành để biến thiết kế thành một hệ thống đáng tin cậy.
