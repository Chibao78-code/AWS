---
title: "Blog 2"
date: 2025-06-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS WAF GIÚP SCALE TO WIN CHỐNG DDoS NHƯ THẾ NÀO?

**Ngày bài nguồn AWS:** 14/07/2025

**Chủ đề:** DDoS, Amazon CloudFront, AWS WAF, rate limiting và CAPTCHA

Trong mùa bầu cử Tổng thống Hoa Kỳ năm 2024, nền tảng Scale to Win trở thành mục tiêu của các đợt DDoS đạt hơn hai triệu request mỗi giây từ gần mười nghìn địa chỉ IP. Sau khoảng gián đoạn ngắn ở giai đoạn đầu, đội ngũ phối hợp với AWS để xây dựng một kiến trúc phòng thủ gồm Amazon CloudFront, AWS WAF và AWS Shield Advanced.

Trường hợp này cho thấy chống DDoS không đơn giản là tăng số máy chủ. Nếu request độc hại vẫn đi đến Application Load Balancer và ứng dụng, backend có thể cạn kết nối hoặc tài nguyên trước khi Auto Scaling phản ứng. Thiết kế hiệu quả cần lọc traffic càng gần edge càng tốt, khóa đường truy cập trực tiếp vào origin và áp dụng chính sách khác nhau cho từng loại client.

## 1. Kiến trúc ban đầu và giới hạn

Ban đầu, DNS của Scale to Win trỏ trực tiếp tới Application Load Balancer. ALB là điểm vào duy nhất và phân phối request đến nhóm EC2 chạy ứng dụng. Cấu trúc này đơn giản nhưng khiến toàn bộ lưu lượng hợp lệ lẫn độc hại đều tiêu thụ năng lực regional của ALB trước khi được xử lý.

Khi DDoS tăng lên hàng triệu request mỗi giây, việc chỉ mở rộng EC2 không giải quyết được lớp mạng và điểm nghẽn tại load balancer. Ngoài chi phí, backend còn phải xử lý TLS, kết nối và request không mang lại giá trị nghiệp vụ.

## 2. Đưa lớp bảo vệ ra AWS Edge

Kiến trúc cập nhật đặt CloudFront và AWS WAF phía trước ALB:

`Người dùng → CloudFront + AWS WAF → Application Load Balancer → EC2`

CloudFront có mạng edge toàn cầu và năng lực xử lý lưu lượng mạng lớn hơn một ALB đơn lẻ. AWS WAF gắn với CloudFront có thể kiểm tra request ngay tại edge, còn AWS Shield Advanced bổ sung bảo vệ và hỗ trợ ứng phó sự kiện DDoS.

Cách bố trí này mang lại ba lợi ích:

* Lưu lượng TCP hoặc HTTP bất thường được hấp thụ ở lớp ngoài trước khi đến VPC.
* Năng lực WAF mở rộng cùng CloudFront, phù hợp với các đợt tăng tải đột ngột.
* Geographic restriction của CloudFront có thể chặn khu vực không phục vụ; trong trường hợp Scale to Win, hơn một nửa traffic độc hại đến từ các quốc gia đã bị chặn, nhờ đó giảm cả request và chi phí WAF.

## 3. Ngăn kẻ tấn công bỏ qua CloudFront

Đặt CloudFront trước ALB chưa đủ nếu endpoint ALB vẫn truy cập trực tiếp được. Kẻ tấn công có thể tìm hostname origin và gửi request thẳng vào đó, bỏ qua toàn bộ rule tại edge.

Scale to Win dùng hai lớp để khóa origin:

1. Security group của ALB chỉ cho phép địa chỉ thuộc CloudFront managed prefix list.
2. CloudFront thêm một custom shared secret header vào request gửi đến origin. ALB listener chỉ forward request khi header khớp; request khác nhận HTTP 403.

Lớp thứ hai rất quan trọng vì kẻ tấn công có thể tự tạo một CloudFront distribution và đặt ALB của nạn nhân làm origin. Managed prefix list sẽ xem request đó đến từ CloudFront, nhưng attacker không có secret hợp lệ. Secret có thể được tạo trong Secrets Manager và xoay vòng bằng Lambda cập nhật đồng thời cấu hình CloudFront và ALB.

## 4. Kết hợp heuristic với giới hạn cứng

Scale to Win không dựa vào một quy tắc duy nhất. Họ sử dụng hai nhóm phát hiện bổ sung cho nhau.

### Heuristic theo mẫu traffic

Đội ngũ xem sample request và AWS WAF log, sau đó tìm đặc điểm phổ biến trong traffic tấn công nhưng hiếm ở request hợp lệ, chẳng hạn header, query parameter, URI hoặc mẫu request body. Rule mới nên chạy với hành động **Count** trước để đo false positive và false negative. Log có thể truy vấn bằng Amazon Athena để liên kết mẫu rule với IP gửi lượng traffic lớn. Khi đủ tin cậy, hành động được chuyển sang **Block**.

Nhược điểm là attacker có thể thay đổi tham số hoặc phát lại request trông giống người dùng thật. Vì vậy heuristic rất hữu ích để phản ứng nhanh nhưng phải được quan sát và điều chỉnh liên tục.

### JA3 và JA4 fingerprint

JA3/JA4 tạo fingerprint từ các thuộc tính TLS ClientHello. Một botnet thường sử dụng số lượng client implementation hạn chế nên có thể để lại một vài fingerprint nổi bật. Tuy nhiên, fingerprint không phải danh tính tuyệt đối: client hợp lệ có thể trùng dấu vân tay và attacker tinh vi có thể xáo trộn thuộc tính TLS. Do đó, JA3/JA4 nên là một tín hiệu kết hợp cùng volume, IP, path và hành vi, không phải rule chặn duy nhất.

### Hard rate limit theo source IP

Rate-based rule của AWS WAF đặt trần request từ một địa chỉ IP trong cửa sổ thời gian. Source IP khó giả mạo trong kết nối TCP/TLS hoàn chỉnh, nên đây là tín hiệu cứng hơn heuristic. Tuy nhiên, không thể đặt một ngưỡng chung quá thấp vì một văn phòng chiến dịch, ký túc xá hoặc trường đại học có thể có hàng trăm người dùng chung NAT IP.

## 5. Tách machine-to-machine và browser traffic

Scale to Win phân loại request theo URI path để tách webhook/API dành cho máy khỏi trang web dành cho người dùng. Việc này cho phép mỗi nhóm có cách xác thực và ngưỡng phù hợp.

### Machine-to-machine traffic

Webhook của Twilio và các API client hợp lệ có thể gửi hàng chục nghìn request từ một số ít IP; chúng không thể giải CAPTCHA. Đối với nhóm này, kiến trúc sử dụng:

* IP set chứa địa chỉ do nhà cung cấp công bố hoặc static proxy để có nguồn ổn định.
* Rule cho phép sớm các path và IP đã xác minh trước khi áp dụng rule dành cho trình duyệt.
* API key, chữ ký request hoặc chứng chỉ khi giao thức hỗ trợ.
* Rate limit theo mức dự kiến của từng client; khi vượt ngưỡng trả HTTP 429 và client retry có kiểm soát.

### Browser traffic

Traffic trình duyệt được áp dụng hai tầng tốc độ:

* Ngưỡng thấp tương ứng với khoảng hai hoặc ba người dùng. Khi vượt ngưỡng, AWS WAF yêu cầu CAPTCHA thay vì chặn ngay.
* Ngưỡng cao tương ứng với trường hợp hợp lệ lớn nhất có hàng trăm người dùng chung IP. Khi vượt mức này, rule Block được áp dụng.

Thứ tự ưu tiên rule phải bảo đảm ngưỡng cao được đánh giá đúng và request đã xác minh CAPTCHA có thể tiếp tục trong phạm vi cho phép. Cấu trúc hai tầng giữ trải nghiệm bình thường cho đa số người dùng, tạo bước xác minh cho vùng nghi ngờ và chỉ chặn traffic vượt quá kịch bản hợp lệ lớn nhất.

## 6. Tích hợp CAPTCHA đúng cách

Thay vì chỉ để WAF trả trang CAPTCHA ở giữa một thao tác, frontend có thể tích hợp AWS WAF CAPTCHA JavaScript API. Người dùng hoàn thành thử thách trong giao diện phù hợp, nhận token và token được gửi cùng các request tiếp theo. Cách này giúp ứng dụng kiểm soát trải nghiệm tốt hơn và hạn chế việc request quan trọng bị thất bại đột ngột.

Tuy nhiên, một token đã giải có thể bị botnet sao chép và phân phối cho nhiều máy. Vì thế, CAPTCHA không thể được xem là tín hiệu đủ mạnh nếu không kiểm tra cách token được sử dụng.

## 7. Ngăn tái sử dụng CAPTCHA token

Scale to Win theo dõi mối quan hệ giữa token và source IP. Nếu cùng một token xuất hiện từ nhiều IP trong thời gian ngắn, khả năng cao token đã bị chia sẻ. AWS WAF label, log và rule tùy chỉnh có thể được dùng để đánh dấu hoặc chặn mẫu này.

Biện pháp này không chỉ hỏi “client có token hợp lệ không?” mà còn hỏi “hành vi sử dụng token có hợp lý không?”. Đây là ví dụ về việc tăng giá trị của cơ chế xác minh bằng ngữ cảnh và tương quan sự kiện.

## 8. Quan sát và điều chỉnh rule

WAF rule không nên được triển khai một lần rồi bỏ mặc. Mỗi rule mới cần giai đoạn Count, dashboard về allowed/blocked/challenged request, log đầy đủ và truy vấn Athena để đánh giá tác động. Đội vận hành nên theo dõi false positive, top source IP, path bị nhắm đến, fingerprint, quốc gia và mức tiêu thụ WAF capacity unit.

Khi chiến thuật tấn công thay đổi, heuristic và ngưỡng cần được cập nhật. Khả năng quan sát giúp điều chỉnh nhanh mà không biến lớp bảo vệ thành nguyên nhân gây gián đoạn cho người dùng hợp lệ.

## 9. Kết quả và giá trị

Kiến trúc cuối cùng có nhiều hàng rào độc lập: Shield và CloudFront hấp thụ lưu lượng, geographic restriction loại bỏ khu vực không phục vụ, WAF phân loại request, security group và shared secret bảo vệ origin, còn rate limit, CAPTCHA và anti-token-reuse kiểm soát hành vi ở lớp ứng dụng.

Thiết kế giúp Scale to Win duy trì dịch vụ trong các sự kiện DDoS lớn, giảm tải cho ALB và EC2, đồng thời vẫn hỗ trợ văn phòng có nhiều người dùng chung IP và webhook có lưu lượng cao. Điều này thể hiện nguyên tắc phòng thủ nhiều lớp: khi attacker vượt qua một tín hiệu, các lớp khác vẫn tiếp tục kiểm soát.

## 10. Điều bản thân rút ra

Từ bài viết, tôi rút ra rằng rate limiting chỉ hiệu quả khi hiểu rõ từng loại traffic. Một ngưỡng chung có thể chặn nhầm webhook hoặc nhóm người dùng sau NAT, trong khi một ngưỡng quá cao lại không đủ chống botnet. Cần phân loại theo path, nguồn và khả năng xác thực, sau đó phối hợp heuristic, giới hạn cứng và CAPTCHA.

Bài học thứ hai là phải khóa origin. Nếu ALB còn đường truy cập trực tiếp, mọi đầu tư vào WAF tại CloudFront đều có thể bị bỏ qua. Cuối cùng, mọi rule bảo mật cần log, thử ở Count mode và có quy trình điều chỉnh; khả năng quan sát là một phần của hệ thống phòng thủ, không phải tính năng bổ sung.

## Liên kết bài viết

* [Bài đăng trên Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2180420536056240/)
* [Bài viết nguồn trên AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/how-scale-to-win-uses-aws-waf-to-block-ddos-events/)
