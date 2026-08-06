---
title: "Event 1"
date: 2026-08-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# BÀI THU HOẠCH SATURDAY MEETUP

## 1. Tổng quan sự kiện

Saturday Meetup là buổi chia sẻ kết hợp giữa kiến thức kỹ thuật, kinh nghiệm phát triển sản phẩm và kỹ năng phát triển bản thân. Nội dung không chỉ tập trung vào cách bắt đầu học AWS an toàn, tiết kiệm mà còn trình bày hành trình xây dựng sản phẩm trong Hackathon, những khó khăn khi duy trì một dự án thực tế và vai trò của sự tự tin trong quá trình học tập.

Điểm có giá trị nhất của sự kiện là các diễn giả trình bày từ trải nghiệm thật. Người tham dự có thể nhìn thấy mối liên hệ giữa việc học một công nghệ, tạo bản thử nghiệm, làm việc trong nhóm và đưa sản phẩm vào vận hành — những giai đoạn mà dự án Splitly cũng đang trải qua.

## 2. Mục tiêu của sự kiện

- Giúp người mới có phương pháp học và thực hành AWS mà vẫn kiểm soát được chi phí.
- Giới thiệu môi trường học có hướng dẫn và công cụ mô phỏng dịch vụ AWS trên máy cá nhân.
- Chia sẻ cách một đội Hackathon biến ý tưởng thành sản phẩm trong thời gian giới hạn.
- Trình bày bài học về triển khai, vận hành và duy trì dự án thực tế.
- Khuyến khích người học chủ động thử thách bản thân và xây dựng sự tự tin.

## 3. Diễn giả

- **Huỳnh Thái Linh**
- **Huỳnh An Khương**
- **Mai Quốc Anh**
- **Nguyễn Trần Minh Quân**
- **Nguyễn Thị Quỳnh Như**
- **Nghĩa Trần**

## 4. Các nội dung chính

### 4.1 Học AWS hiệu quả và tránh chi phí ngoài dự kiến

Phần chia sẻ của anh Huỳnh Thái Linh bắt đầu từ nỗi lo phổ biến của người mới: sợ dùng quá ngân sách, quên xóa tài nguyên hoặc chưa dám thử dịch vụ vì không biết khoản phí sẽ phát sinh như thế nào. Vấn đề không nằm ở việc ngừng thực hành, mà ở cách lựa chọn môi trường học và xây dựng thói quen quản lý tài nguyên.

Hai hướng tiếp cận được giới thiệu:

- **AWS Cloud Quest:** môi trường học theo nhiệm vụ, kết hợp bài lab và yếu tố trò chơi hóa. Người học có thể thực hành theo một lộ trình rõ ràng trước khi tự xây dựng hạ tầng riêng.
- **Floci:** công cụ mô phỏng một số dịch vụ AWS trên máy cục bộ, phù hợp để thử logic ứng dụng hoặc quy trình tích hợp trước khi triển khai lên tài khoản AWS thật.

Khi so sánh với LocalStack, Floci được nhắc đến với các ưu điểm như tốc độ, mức sử dụng tài nguyên và mô hình sử dụng thuận lợi trong một số trường hợp. Tuy nhiên, các môi trường giả lập chỉ hỗ trợ một phần dịch vụ, có thể trả về dữ liệu mock và không tái hiện hoàn toàn IAM, networking, quota hoặc hành vi của AWS thật. Vì vậy, chúng phù hợp cho giai đoạn phát triển sớm nhưng không thay thế bước kiểm thử cuối trên AWS.

Bài học thực tế là phải kết hợp nhiều lớp kiểm soát: dùng môi trường mô phỏng khi phù hợp, đặt ngân sách/cảnh báo, gắn tag và luôn có checklist dọn dẹp sau mỗi bài lab.

### 4.2 Hành trình Hackathon và dự án SynthHunter

Anh Huỳnh An Khương, anh Mai Quốc Anh và anh Nguyễn Trần Minh Quân chia sẻ quá trình tham gia Hackathon và phát triển **SynthHunter**. Câu chuyện tập trung vào toàn bộ vòng đời ngắn của một sản phẩm: lựa chọn vấn đề, hình thành ý tưởng, thống nhất phạm vi, phân chia nhiệm vụ, xây dựng kiến trúc và hoàn thiện bản trình diễn trong thời gian giới hạn.

Qua phần trình bày kiến trúc và cách phối hợp của nhóm, có thể rút ra rằng một ý tưởng tốt vẫn cần được chuyển thành các đầu việc có thứ tự ưu tiên. Trong Hackathon, nhóm không thể làm mọi tính năng; thành công phụ thuộc vào việc xác định giá trị cốt lõi, tạo một luồng hoạt động xuyên suốt và xử lý sớm các rủi ro quan trọng.

Phần này cũng làm rõ vai trò của giao tiếp và quản lý thời gian. Các thành viên cần hiểu ranh giới trách nhiệm nhưng vẫn thường xuyên tích hợp kết quả, vì một thành phần hoàn thành riêng lẻ chưa bảo đảm sản phẩm cuối cùng hoạt động.

### 4.3 Xây dựng sự tự tin trong học tập

Phần chia sẻ của chị Nguyễn Thị Quỳnh Như phân tích cách sự thiếu tự tin có thể khiến người học bỏ lỡ cơ hội, tránh thử thách và dễ dừng lại khi gặp khó khăn. Những nguyên nhân thường gặp là sợ thất bại, sợ bị đánh giá và chỉ quan tâm đến kết quả cuối cùng thay vì quá trình tiến bộ.

Quy tắc 5P được giới thiệu như một khung thực hành để từng bước vượt qua nỗi sợ. Bên cạnh đó, diễn giả đề xuất bắt đầu với mục tiêu nhỏ, ghi nhận thành quả hằng ngày, duy trì thái độ học liên tục và ưu tiên sự tiến bộ hơn sự hoàn hảo.

Thông điệp quan trọng là sự tự tin không đồng nghĩa với việc luôn biết câu trả lời. Sự tự tin được hình thành khi người học dám thực hiện, quan sát kết quả, nhận phản hồi và tiếp tục cải thiện.

### 4.4 Kinh nghiệm phát triển dự án thực tế TuviDaiviet

Anh Nghĩa Trần chia sẻ kinh nghiệm xây dựng và duy trì **TuviDaiviet**. Khác với một bản demo, sản phẩm thực tế phải đối mặt với lỗi kỹ thuật, yêu cầu vận hành, phản hồi người dùng và nhu cầu cải tiến liên tục.

Qua những khó khăn và cơ hội xuất hiện trong quá trình phát triển, phần chia sẻ cho thấy công việc không kết thúc khi tính năng được lập trình xong. Nhóm còn cần quan tâm đến triển khai, theo dõi hệ thống, xử lý sự cố, bảo trì và đưa phản hồi thực tế trở lại kế hoạch sản phẩm.

## 5. Kiến thức và kỹ năng học được

### Kiến thức kỹ thuật

- Hiểu cách kết hợp AWS Cloud Quest, môi trường giả lập và tài khoản AWS thật theo từng giai đoạn học.
- Nhận biết giới hạn của công cụ mô phỏng và lý do phải kiểm thử lại IAM, networking và luồng dữ liệu trên môi trường thật.
- Biết rằng quản lý chi phí cần được thực hiện từ đầu bằng ngân sách, cảnh báo, tag và quy trình xóa tài nguyên.
- Có thêm góc nhìn về cách lựa chọn kiến trúc tối thiểu để hoàn thành sản phẩm trong Hackathon.
- Hiểu rằng triển khai, giám sát và bảo trì là một phần của vòng đời sản phẩm, không phải công việc tách rời sau phát triển.

### Kỹ năng và tư duy

- Xác định phạm vi sản phẩm dựa trên giá trị cốt lõi thay vì cố gắng hoàn thành mọi ý tưởng.
- Chia nhỏ công việc, phân công rõ ràng và tích hợp kết quả thường xuyên.
- Quản lý thời gian khi phải làm việc dưới áp lực deadline.
- Xem lỗi và phản hồi như dữ liệu để cải thiện sản phẩm.
- Xây dựng sự tự tin thông qua những bước tiến nhỏ và quá trình thực hành liên tục.

## 6. Áp dụng vào dự án Splitly

Những nội dung của meetup có thể áp dụng trực tiếp vào quá trình phát triển Splitly:

1. **Kiểm soát chi phí AWS:** cấu hình AWS Budgets, theo dõi public IPv4/EC2 và dùng checklist dọn dẹp CloudFormation sau thực hành.
2. **Kiểm thử trước khi triển khai:** có thể mô phỏng một số thao tác S3 trong môi trường local, nhưng phải kiểm tra lại IAM Role, bucket policy và presigned URL trên AWS thật.
3. **Ưu tiên MVP:** tập trung trước vào đăng nhập, tạo nhóm, ghi nhận khoản chi, tính số dư, settlement và biên lai; các tính năng mở rộng chỉ thực hiện sau khi luồng chính ổn định.
4. **Phân chia trách nhiệm:** tách đầu việc frontend, backend, dữ liệu, AWS và tài liệu, đồng thời quy định thời điểm tích hợp chung để tránh xung đột cuối kỳ.
5. **Vận hành sản phẩm:** dùng PM2 và CloudWatch để theo dõi lỗi, ghi lại quy trình triển khai/khôi phục và xem phản hồi người dùng là đầu vào cho phiên bản tiếp theo.
6. **Tư duy thử nghiệm:** triển khai từng thay đổi nhỏ, kiểm chứng bằng dữ liệu và sẵn sàng điều chỉnh thay vì chờ một phiên bản hoàn hảo.

## 7. Cảm nhận sau sự kiện

Sự kiện giúp mình nhận ra học công nghệ hiệu quả cần đồng thời ba yếu tố: môi trường thực hành phù hợp, khả năng hợp tác để tạo ra sản phẩm và tư duy đủ bền bỉ để vượt qua sai sót. Phần AWS mang lại các cách thực hành an toàn hơn; câu chuyện SynthHunter cho thấy giá trị của phạm vi rõ ràng và làm việc nhóm; phần tự tin nhắc rằng sự tiến bộ đến từ hành động; còn TuviDaiviet cung cấp góc nhìn thực tế về trách nhiệm sau khi sản phẩm được phát hành.

![Hình ảnh tại Event 1](/images/4-Event/Splitly/event-1-pic.jpg)

> Sau meetup, bài học lớn nhất của mình là một sản phẩm tốt không chỉ được đánh giá bằng số lượng tính năng. Nó còn phụ thuộc vào khả năng kiểm soát chi phí, phối hợp nhóm, vận hành ổn định và liên tục cải thiện từ phản hồi thực tế.
