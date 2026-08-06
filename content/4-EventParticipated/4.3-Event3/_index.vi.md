---
title: "Event 3"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# BÀI THU HOẠCH AGENT FORGE – DEEPDIVE DAY 1

## 1. Thông tin sự kiện

- **Chủ đề:** Agent Forge – Deepdive Day 1.
- **Chuỗi chương trình:** 3-Day AgentForge Workshop.
- **Thời gian:** 09:00–12:00, Thứ Bảy ngày 01/08/2026 (GMT+7).
- **Địa điểm:** [Bitexco Financial Tower, Thành phố Hồ Chí Minh](https://www.google.com/maps/search/?api=1&query=Bitexco%20Financial%20Tower&query_place_id=ChIJ6-qHzzovdTERKuM7X5ehack).
- **Lĩnh vực:** Artificial Intelligence và AWS.
- **Vai trò:** Người tham dự workshop.

Day 1 tập trung vào **Foundations & Agent Setup**, giúp người tham dự đi từ khái niệm Amazon Bedrock AgentCore đến một luồng triển khai agent cơ bản có tool, nguồn tri thức, giao diện web và xác thực người dùng.

## 2. Mục tiêu của buổi workshop

- Hiểu vai trò của Amazon Bedrock AgentCore trong vòng đời một AI agent.
- Phân biệt trách nhiệm của Runtime, Gateway và Identity.
- Triển khai một agent cơ bản lên môi trường được quản lý.
- Kết nối agent với external tool và Knowledge Base thay vì chỉ sinh văn bản độc lập.
- Xây dựng giao diện web để người dùng tương tác với agent.
- Tích hợp Amazon Cognito để xác thực trước khi cho phép truy cập ứng dụng.
- Hình thành tư duy bảo mật khi agent có khả năng gọi công cụ và thao tác dữ liệu.

## 3. Nội dung nền tảng: Amazon Bedrock AgentCore

Phần đầu của sự kiện giới thiệu tổng quan AgentCore và ba thành phần chính xuất hiện trong agenda.

### 3.1 AgentCore Runtime

Runtime là môi trường chạy mã agent hoặc tool. Thay vì tự xây dựng toàn bộ máy chủ, cơ chế mở rộng và quản lý phiên, nhóm phát triển đóng gói logic agent rồi triển khai lên Runtime. Mỗi runtime có định danh và phiên bản riêng, hỗ trợ cập nhật có kiểm soát.

Điều quan trọng mình rút ra là “model” và “agent runtime” không phải một khái niệm. Model tạo phản hồi, còn runtime chịu trách nhiệm nhận request, duy trì ngữ cảnh phiên, thực thi logic và phối hợp việc gọi công cụ.

### 3.2 AgentCore Gateway

Gateway tạo một điểm truy cập thống nhất để agent tìm và gọi tool, API hoặc dịch vụ khác. Thay vì cho agent kết nối trực tiếp tới từng hệ thống với cách xác thực khác nhau, Gateway chuẩn hóa cách công bố target và kiểm soát lưu lượng đi qua.

Trong một thiết kế tốt, tool phải có mô tả rõ, input được kiểm tra và quyền bị giới hạn theo chức năng. Gateway giúp tổ chức các tool, nhưng đội phát triển vẫn phải quyết định agent được phép gọi tool nào và hành động nào cần xác nhận từ người dùng.

### 3.3 AgentCore Identity

Identity giải quyết hai hướng xác thực. Ở chiều vào, hệ thống cần biết người dùng hoặc ứng dụng nào được phép gọi agent. Ở chiều ra, agent cần credential phù hợp để truy cập tool, AWS resource hoặc dịch vụ bên thứ ba mà không để khóa bí mật trong mã nguồn.

Khái niệm workload identity giúp agent có danh tính riêng để áp dụng chính sách và lưu vết. Điều này đặc biệt quan trọng khi agent thực hiện hành động thay mặt người dùng, vì hệ thống cần tách quyền của agent, quyền của người dùng và quyền của dịch vụ đích.

## 4. Bài thực hành

### 4.1 Triển khai agent cơ bản

Phần lab bắt đầu bằng việc chuẩn bị logic agent và đưa agent lên AgentCore Runtime. Qua bước này, người tham dự có thể hình dung luồng từ mã nguồn đến một endpoint có thể được giao diện hoặc ứng dụng khác gọi.

Các điểm cần quan sát khi triển khai gồm execution role, Region, dependency, cấu hình runtime và log. Một agent chạy được chưa đồng nghĩa với sẵn sàng production; vẫn cần kiểm thử lỗi, timeout, giới hạn quyền và hành vi khi tool không phản hồi.

### 4.2 Kết nối external tool và Knowledge Base

Agent trở nên hữu ích hơn khi có thể truy xuất thông tin hoặc gọi một chức năng bên ngoài. External tool cung cấp hành động có cấu trúc, còn Knowledge Base bổ sung nguồn dữ liệu để câu trả lời bám sát nội dung được quản lý.

Phần này giúp mình phân biệt hai mục đích:

- **Knowledge Base** phù hợp với câu hỏi cần tìm thông tin, tài liệu hoặc hướng dẫn.
- **Tool** phù hợp với thao tác như gọi API, tra cứu dữ liệu động hoặc thực hiện một nghiệp vụ cụ thể.

Agent không nên được cấp quyền truy cập database hoặc API quá rộng. Một tool nhỏ, có input/output rõ và chỉ thực hiện đúng một chức năng sẽ dễ kiểm thử và kiểm soát hơn.

### 4.3 Xây dựng Web UI và tích hợp Amazon Cognito

Web UI cung cấp giao diện để gửi yêu cầu và hiển thị phản hồi của agent. Amazon Cognito được tích hợp để người dùng đăng nhập trước khi truy cập, sau đó token xác thực được sử dụng trong luồng gọi agent.

Phần xác thực làm rõ rằng giao diện chat chỉ là lớp bên ngoài. Phía sau vẫn cần kiểm tra token, xác định danh tính, giới hạn dữ liệu theo người dùng và không tin tưởng input chỉ vì request đến từ frontend của mình.

## 5. Luồng kiến trúc hiểu được từ workshop

Một request có thể được hình dung theo trình tự:

1. Người dùng đăng nhập trên Web UI thông qua Amazon Cognito.
2. Web UI gửi request kèm token tới agent.
3. AgentCore Runtime xác thực request và chạy logic agent trong phiên tương ứng.
4. Khi cần hành động, agent gọi tool thông qua AgentCore Gateway.
5. AgentCore Identity cung cấp hoặc kiểm soát credential cần thiết cho agent/tool.
6. Tool truy cập API, AWS resource hoặc Knowledge Base trong phạm vi được phép.
7. Kết quả quay lại Runtime, được agent tổng hợp và trả về Web UI.

Luồng này cho thấy bảo mật không nằm ở một thành phần duy nhất. Cognito xác thực người dùng, Runtime bảo vệ endpoint thực thi, Gateway quản lý đường tới tool, còn Identity quản lý danh tính và credential của workload.

## 6. Kiến thức và kỹ năng học được

### Kiến thức kỹ thuật

- Phân biệt model, agent, runtime, gateway, identity, tool và Knowledge Base.
- Hiểu một agent production cần lớp thực thi, xác thực và tích hợp chứ không chỉ cần prompt.
- Biết cách chia khả năng của agent thành các tool có hợp đồng rõ ràng.
- Nhận thức được sự khác nhau giữa inbound authentication và outbound authentication.
- Hiểu vai trò của Cognito trong việc bảo vệ Web UI và luồng gọi backend.
- Chú ý đến least privilege, log, timeout, lỗi tool và khả năng audit hành động của agent.

### Tư duy thiết kế

- Bắt đầu từ một use case nhỏ có thể đo lường thay vì tạo agent có quyền quá rộng.
- Tách dữ liệu tham khảo khỏi hành động thay đổi trạng thái.
- Yêu cầu người dùng xác nhận trước các thao tác nhạy cảm hoặc khó hoàn tác.
- Đánh giá chất lượng bằng độ chính xác, tỷ lệ hoàn thành tác vụ, độ trễ, chi phí và mức an toàn.
- Không coi giao diện trò chuyện là bằng chứng rằng hệ thống đã được bảo mật đầy đủ.

## 7. Khả năng áp dụng vào Splitly

AgentCore chưa cần thiết cho phiên bản Splitly hiện tại, nhưng workshop gợi mở một hướng mở rộng hợp lý: **trợ lý chi tiêu nhóm**.

Một phiên bản thử nghiệm có thể hỗ trợ:

- Trả lời câu hỏi như “Nhóm đã chi nhiều nhất cho hạng mục nào?” hoặc “Khoản nào chưa được đối soát?”.
- Tìm hướng dẫn sử dụng Splitly từ Knowledge Base.
- Gọi các tool chỉ đọc như `getGroupSummary`, `listUnsettledExpenses` hoặc `findReceiptMetadata`.
- Giải thích kết quả chia tiền dựa trên dữ liệu đã có, nhưng không tự ý sửa giao dịch.

Nếu phát triển chức năng này, nhóm nên áp dụng các nguyên tắc:

1. Cognito hoặc hệ thống xác thực hiện có phải xác định đúng người dùng.
2. Mỗi request chỉ được truy cập nhóm mà người dùng là thành viên.
3. Agent gọi API nghiệp vụ có kiểm soát, không kết nối trực tiếp MongoDB bằng quyền rộng.
4. Tool thay đổi khoản chi hoặc settlement phải yêu cầu xác nhận rõ ràng.
5. Dữ liệu biên lai và thông tin tài chính không được đưa vào log/prompt ngoài phạm vi cần thiết.
6. Tính năng agent chỉ được bổ sung sau khi các chức năng chia tiền cốt lõi đã ổn định.

## 8. Trải nghiệm và cảm nhận

Event có thời lượng ngắn nhưng cấu trúc hợp lý: bắt đầu bằng ba thành phần nền tảng, sau đó chuyển ngay sang triển khai agent, kết nối công cụ và hoàn thiện giao diện có xác thực. Cách tổ chức này giúp mình nhìn AgentCore như một hệ thống gồm nhiều lớp trách nhiệm thay vì chỉ là một dịch vụ AI đơn lẻ.

![Hình ảnh tại Agent Forge – Deepdive Day 1](/images/4-Event/Splitly/event-3-pic.jpg)

> Bài học quan trọng nhất của mình là khi AI agent có khả năng gọi công cụ, thiết kế identity và quyền truy cập phải được xem là một phần của chức năng ngay từ đầu. Agent hữu ích không chỉ cần trả lời tốt mà còn phải hành động đúng phạm vi, có thể theo dõi và an toàn đối với dữ liệu người dùng.

## 9. Tài liệu đối chiếu

- [Amazon Bedrock AgentCore Runtime – How it works](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-how-it-works.html)
- [Amazon Bedrock AgentCore Gateway](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html)
- [Amazon Bedrock AgentCore Identity](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/identity.html)
