---
title: "Blog 3"
date: 2026-03-26
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# KIẾN TRÚC HỆ THỐNG HỖ TRỢ PHÁT TRIỂN AGENTIC AI TRÊN AWS

**Ngày bài nguồn AWS:** 26/03/2026

**Chủ đề:** Agentic AI, vòng phản hồi, kiến trúc codebase, kiểm thử và CI/CD

AI coding assistant có thể gợi ý mã, còn AI agent có thể nhận một mục tiêu lớn hơn, chỉnh sửa nhiều tệp, chạy kiểm thử, triển khai và tiếp tục sửa dựa trên kết quả. Tuy nhiên, khả năng tạo mã nhanh không tự động làm chu kỳ phát triển nhanh. Nếu mỗi lần xác minh đều phải chờ cấp phát cloud, chạy pipeline dài hoặc nhờ con người kiểm tra thủ công, agent chỉ tạo ra một hàng đợi thay đổi nhanh hơn chứ chưa tạo ra phần mềm đáng tin cậy nhanh hơn.

Bài viết này phân tích hai mặt phải thay đổi đồng thời: **system architecture** cần cung cấp vòng phản hồi ngắn và môi trường dùng tạm; **codebase architecture** cần có ranh giới, quy tắc và bằng chứng kiểm thử đủ rõ để agent hiểu ý định của con người.

## 1. Vì sao kiến trúc truyền thống cản trở agent

Nhiều hệ thống cloud được thiết kế cho quy trình do con người điều khiển: môi trường tồn tại lâu, release không thường xuyên, kiểm thử tích hợp sau khi triển khai và kiến thức vận hành nằm trong kinh nghiệm của một vài kỹ sư. Mô hình này tạo ra các điểm nghẽn đối với agent:

* Logic nghiệp vụ kết dính trực tiếp với SDK và dịch vụ cloud nên không thể kiểm thử cục bộ.
* Mỗi thay đổi cần một stack đầy đủ, tạo độ trễ và chi phí lớn cho các lần thử chưa chắc đúng.
* Cấu trúc repository không nhất quán khiến agent khó xác định tệp cần sửa và phạm vi ảnh hưởng.
* API và quy tắc kiến trúc chỉ được truyền miệng, làm thay đổi dễ phá vỡ hợp đồng giữa dịch vụ.
* Test chậm hoặc thiếu test khiến agent không có tín hiệu khách quan để tự sửa sai.

Vì vậy, giải pháp không chỉ là viết prompt chi tiết hơn. Kiến trúc phải xem khả năng xác minh nhanh và an toàn là yêu cầu nền tảng.

## 2. Vòng phản hồi nhiều tầng

Một workflow phù hợp với Agentic AI không dùng cloud production làm nơi thử đầu tiên. Thay vào đó, thay đổi đi qua các vòng phản hồi có chi phí tăng dần:

1. Format, lint, type-check và unit test chạy ngay trên máy phát triển.
2. Mô phỏng dịch vụ hoặc container cục bộ để kiểm tra luồng tích hợp chính.
3. Stack cloud tối thiểu xác nhận hành vi của dịch vụ AWS không thể mô phỏng đầy đủ.
4. Preview environment chạy smoke test và end-to-end test.
5. CI/CD áp dụng kiểm tra bảo mật, review, approval và triển khai theo chính sách.

Agent nhận phản hồi rẻ và nhanh trước, chỉ sử dụng tài nguyên cloud khi thay đổi đã vượt qua các kiểm tra cơ bản. Cấu trúc này giảm thời gian, chi phí và rủi ro của mỗi vòng lặp.

## 3. Mô phỏng cục bộ làm đường kiểm tra mặc định

### Ứng dụng serverless

Với AWS Lambda và Amazon API Gateway, AWS Serverless Application Model (AWS SAM) có thể chạy API cục bộ bằng `sam local start-api`. Agent có thể gọi endpoint, quan sát response và log, sửa mã rồi chạy lại trong vài giây. Unit test vẫn xử lý logic nhỏ nhất, còn SAM kiểm tra wiring, event shape và handler gần với môi trường Lambda hơn.

### Ứng dụng container

Ứng dụng dự kiến chạy trên Amazon ECS hoặc AWS Fargate nên dùng cùng Dockerfile để build và chạy local. Agent có thể kiểm tra startup, health endpoint, biến môi trường, dependency và hành vi request trước khi push image. Việc dùng cùng artifact giúp giảm chênh lệch “chạy trên máy nhưng lỗi khi deploy”.

### Lưu trữ dữ liệu

DynamoDB Local cung cấp API tương thích cho các thao tác create, read, update và delete. Agent có thể tạo bảng mẫu, seed dữ liệu, kiểm tra repository và reset trạng thái nhanh. Điều quan trọng là cô lập lớp truy cập dữ liệu sau interface để test domain không phụ thuộc vào database, còn integration test có thể thay adapter local bằng adapter AWS thật.

Mô phỏng không bảo đảm giống cloud tuyệt đối, nhưng nó là lớp phản hồi đầu tiên có tốc độ cao. Các khác biệt còn lại được kiểm tra ở tầng hybrid và preview.

## 4. Phát triển ngoại tuyến cho dữ liệu và phân tích

Pipeline dữ liệu thường khó kiểm thử vì phụ thuộc dataset lớn và runtime phân tán. AWS Glue cung cấp Docker image chứa thư viện ETL để chạy job cục bộ. Agent có thể dùng tập dữ liệu nhỏ có trường hợp biên, kiểm tra schema, transformation và kết quả trung gian trước khi gửi job lên cloud.

Nguyên tắc chung là tách logic biến đổi thuần khỏi phần đọc/ghi dịch vụ. Test cục bộ xác minh quy tắc xử lý dữ liệu; cloud run sau đó tập trung vào khả năng mở rộng, quyền truy cập, partition và hiệu suất. Nhờ vậy, các lỗi logic đơn giản không tiêu tốn một lần chạy Glue hoàn chỉnh.

## 5. Kiểm thử hybrid với tài nguyên cloud gọn nhẹ

Một số hành vi của Amazon SNS, Amazon SQS, IAM hoặc network policy không thể mô phỏng hoàn toàn. Trong trường hợp đó, Infrastructure as Code bằng AWS CloudFormation hoặc AWS CDK tạo một stack nhỏ, độc lập theo nhánh hoặc task.

Agent có thể triển khai queue, topic, role và thành phần tối thiểu; gọi chúng qua AWS SDK; xác minh event, retry, dead-letter behavior và quyền; sau đó hủy stack. Môi trường phải có tên duy nhất, tag chủ sở hữu, thời hạn tự dọn và giới hạn quyền để tránh tài nguyên mồ côi hoặc truy cập nhầm dữ liệu thật.

Cloud lúc này trở thành một dependency kiểm thử có kiểm soát, không phải môi trường thủ công duy nhất mà mọi thay đổi phải chia sẻ.

## 6. Preview environment và contract-first design

Khi nhiều dịch vụ tương tác, preview environment cung cấp một stack ngắn hạn cho toàn bộ nhánh hoặc pull request. Pipeline tạo môi trường bằng IaC, triển khai artifact, chạy smoke/end-to-end test và xóa tài nguyên khi hoàn tất. Mỗi thay đổi được kiểm tra cách ly nên không làm hỏng môi trường tích hợp chung.

Contract-first design định nghĩa API trước bằng OpenAPI, schema sự kiện hoặc interface versioned. Client và server có thể sinh mock, contract test và triển khai song song. Agent biết rõ input, output, error code và versioning rule, nên ít tự suy đoán hơn khi sửa nhiều dịch vụ.

Khi kết hợp preview với contract test, hệ thống vừa kiểm tra từng dịch vụ tôn trọng hợp đồng, vừa xác minh luồng thực tế trên cloud trước production.

## 7. Codebase thân thiện với AI

Tốc độ môi trường không đủ nếu repository khó hiểu. Một codebase phù hợp cần tên thư mục dự đoán được, module nhỏ, dependency có hướng và command chuẩn cho build/test.

### Ranh giới domain, application và infrastructure

Cấu trúc lấy cảm hứng từ Domain-Driven Design và hexagonal architecture có thể chia thành:

* `/domain`: entity, value object và business rule không phụ thuộc AWS.
* `/application`: use case và orchestration, làm việc qua interface/port.
* `/infrastructure`: adapter cho DynamoDB, SNS, SQS, HTTP và SDK AWS.
* `/interfaces` hoặc `/api`: handler, controller và schema giao tiếp bên ngoài.

Dependency hướng vào domain, còn dịch vụ ngoài được kết nối qua adapter. Agent có thể thay đổi business rule và chạy unit test mà không cần credential AWS. Khi chỉnh adapter, phạm vi ảnh hưởng và integration test cần chạy cũng rõ hơn.

## 8. Mã hóa ý định bằng project rules

Tên thư mục thể hiện cấu trúc, nhưng chưa giải thích toàn bộ quyết định. Repository nên lưu các tệp hướng dẫn ngắn và cụ thể, ví dụ:

* Chỉ lớp infrastructure được import AWS SDK.
* Mọi truy cập database phải đi qua repository interface.
* API public phải cập nhật OpenAPI và contract test.
* Tài nguyên cloud phải khai báo bằng IaC, có tag và cơ chế cleanup.
* Không tự động thay đổi IAM production hoặc xóa dữ liệu nếu chưa có phê duyệt.

Các tệp như `AGENTS.md`, `CONTRIBUTING.md`, `RUNBOOK.md` hoặc steering file của Kiro giúp agent đọc quy tắc ngay trong repository. Hướng dẫn nên trỏ đến command có thể chạy và ví dụ ngắn, tránh tài liệu dài nhưng không kiểm chứng được.

## 9. Kiểm thử như đặc tả có thể thực thi

Trong workflow agentic, test vừa bắt regression vừa mô tả hành vi mong muốn.

* **Unit test** xác minh domain logic độc lập, chạy nhanh sau từng thay đổi nhỏ.
* **Contract test** xác minh producer và consumer tuân theo OpenAPI hoặc event schema, phát hiện breaking change trước khi triển khai chung.
* **Integration test** kiểm tra adapter, database và message flow ở local hoặc stack hybrid.
* **Smoke test** chạy trên preview để phát hiện lỗi chỉ xuất hiện khi deploy, như thiếu IAM permission, sai environment variable hoặc cấu hình route.

Khi test thất bại với thông báo rõ, agent có thể so sánh expected/actual và tiếp tục sửa. Test mơ hồ hoặc flaky tạo vòng lặp sai, vì vậy độ ổn định và khả năng chẩn đoán của test quan trọng không kém độ bao phủ.

## 10. Monorepo và tài liệu máy có thể đọc

Monorepo giúp agent thấy service, thư viện chia sẻ, IaC và contract trong cùng một ngữ cảnh, từ đó đánh giá tác động xuyên hệ thống. Nếu dùng nhiều repository, cần cơ chế cung cấp contract và version map tương đương.

Tài liệu nên ưu tiên cấu trúc mà công cụ có thể phân tích: YAML/JSON schema, OpenAPI, package manifest, task runner và command thống nhất. Sơ đồ và prose vẫn hữu ích cho con người, nhưng trạng thái có thể kiểm tra bằng máy giúp agent xác minh thay vì đoán.

## 11. Tích hợp agent an toàn vào CI/CD

Agent có thể tạo branch, sửa mã và mở pull request, nhưng pipeline vẫn phải là ranh giới thực thi chính sách. Guardrail phù hợp gồm:

* Format, lint, type-check, unit/contract/integration test bắt buộc.
* Static analysis, dependency scan, secret scan và kiểm tra IaC.
* Branch protection và review cho mã ảnh hưởng production.
* Credential ngắn hạn, least privilege và tách tài khoản development khỏi production.
* Manual approval cho IAM, network, migration dữ liệu và thao tác phá hủy.
* Log đầy đủ về thay đổi, lệnh đã chạy, artifact và kết quả triển khai.

Mức tự chủ có thể tăng dần khi đội ngũ có dữ liệu chứng minh quy trình ổn định. Agent có thể tự xử lý thay đổi rủi ro thấp, trong khi con người vẫn quyết định những thay đổi có blast radius lớn.

## 12. Kết quả và giá trị

Khi hệ thống được thiết kế theo các nguyên tắc trên, thời gian xác minh thay đổi giảm từ hàng chục phút xuống vài giây ở vòng local, còn cloud chỉ được dùng cho những điểm cần độ trung thực cao hơn. Agent nhận được tín hiệu rõ để tự sửa, chi phí môi trường thử nghiệm giảm và lỗi tích hợp được phát hiện trước production.

Đội phát triển cũng hưởng lợi dù không dùng AI: module rõ ràng hơn, onboarding nhanh hơn, test đáng tin cậy hơn và preview environment giảm xung đột giữa các nhóm. Kiến trúc phục vụ agent thực chất là kiến trúc có khả năng tự giải thích và tự kiểm chứng tốt hơn.

## 13. Điều bản thân rút ra

Hiệu quả của Agentic AI không chỉ phụ thuộc vào model. Model mạnh nhưng phải chờ pipeline lâu, thiếu test và không hiểu ranh giới kiến trúc vẫn tạo ra kết quả chậm và rủi ro. Nền tảng quyết định mức agent có thể hoạt động độc lập chính là feedback loop, code boundary, executable specification và guardrail.

Tôi cũng nhận thấy mục tiêu không phải loại bỏ con người khỏi quy trình. Tự động hóa nên xử lý vòng lặp nhỏ, lặp lại và có thể xác minh; con người tập trung vào mục tiêu, trade-off, dữ liệu nhạy cảm và quyết định có ảnh hưởng lớn. Đây là cách dùng agent như một hệ số nhân năng suất mà không đánh đổi khả năng kiểm soát.

## Liên kết bài viết

* [Bài đăng trên Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2201707250594235/?rdid=Le865pC3R2JaAgDY#)
* [Bài viết nguồn trên AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/architecting-for-agentic-ai-development-on-aws/)
