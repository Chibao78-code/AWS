---
title: "Bản đề xuất"
date: 2026-08-06
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# SPLITLY – NỀN TẢNG QUẢN LÝ CHI TIÊU NHÓM

## Giải pháp triển khai trên AWS cho việc ghi nhận, phân chia và đối soát chi phí

## 1. Tóm tắt đề xuất

Splitly được xây dựng để giải quyết một tình huống quen thuộc: nhiều người cùng tham gia chuyến đi, sự kiện hoặc sinh hoạt chung nhưng mỗi khoản tiền lại do một thành viên khác nhau thanh toán. Khi dữ liệu nằm rải rác trong tin nhắn, bảng tính và ảnh chụp hóa đơn, việc xác định ai đã trả, ai còn nợ và cần hoàn tiền như thế nào dễ xảy ra sai sót.

Đề xuất này đưa Splitly lên AWS dưới dạng một ứng dụng web tập trung. Frontend sử dụng React, TypeScript và Vite; backend sử dụng Node.js, Express và TypeScript; dữ liệu nghiệp vụ nằm trong MongoDB Atlas. Ở giai đoạn hiện tại, frontend và backend cùng được triển khai trên một Amazon EC2 để phù hợp với quy mô và ngân sách của dự án sinh viên. Amazon S3 lưu ảnh biên lai, Amazon CloudWatch hỗ trợ giám sát, Amazon SNS chuyển cảnh báo và AWS Budgets theo dõi chi phí.

Mục tiêu của dự án không chỉ là đưa website lên Internet mà còn hình thành một quy trình triển khai có thể lặp lại, có kiểm soát quyền truy cập, có log để chẩn đoán và có phương án mở rộng khi số người dùng tăng.

## 2. Bài toán, người dùng và phạm vi

### 2.1 Bài toán cần giải quyết

Các phương pháp quản lý chi phí nhóm thủ công thường gặp các hạn chế:

- Một nhóm có nhiều khoản chi và nhiều người thanh toán nên khó theo dõi số dư tổng thể.
- Công thức chia tiền có thể không đồng đều, dễ tính nhầm khi cập nhật hoặc hủy một khoản chi.
- Trạng thái hoàn tiền không rõ ràng, dẫn đến đối soát nhiều lần.
- Ảnh hóa đơn nằm rải rác và khó tìm lại khi phát sinh tranh luận.
- Khi ứng dụng gặp lỗi sau triển khai, nhóm thiếu metric, log và cảnh báo để xác định nguyên nhân.

### 2.2 Nhóm người dùng

- **Thành viên:** tham gia nhóm, xem khoản chi và số dư liên quan đến mình.
- **Người thanh toán/người tạo chi phí:** nhập số tiền, lựa chọn người tham gia, cách chia và tải biên lai.
- **Quản trị nhóm:** quản lý thành viên, điều chỉnh dữ liệu phù hợp với quyền được cấp và theo dõi quá trình đối soát.
- **Quản trị hệ thống:** triển khai phiên bản mới, theo dõi tài nguyên, xử lý sự cố và kiểm soát chi phí AWS.

### 2.3 Chức năng trong phạm vi

- Đăng ký, đăng nhập và quản lý thông tin người dùng.
- Tạo nhóm, mời hoặc thêm thành viên và quản lý vai trò cơ bản.
- Ghi nhận khoản chi, người trả tiền, đối tượng tham gia và quy tắc phân chia.
- Tính số dư, gợi ý nghĩa vụ hoàn tiền và theo dõi trạng thái settlement.
- Lưu trữ biên lai điện tử trên Amazon S3 và liên kết metadata với giao dịch.
- Quản lý thông báo, khiếu nại hoặc điều chỉnh liên quan đến khoản chi.
- Tích hợp Gmail và VNPay Sandbox khi thông tin cấu hình được cung cấp.
- Thu thập log/metric, gửi cảnh báo vận hành và cảnh báo ngân sách.

### 2.4 Ngoài phạm vi giai đoạn hiện tại

Kiến trúc đa vùng, Auto Scaling, cân bằng tải, ứng dụng di động native và xử lý thanh toán production chưa nằm trong phạm vi triển khai hiện tại. CloudFront, Route 53, AWS WAF, ACM và việc tách frontend ra khỏi EC2 được xem là giai đoạn nâng cấp tiếp theo.

## 3. Kiến trúc giải pháp hiện tại

![Kiến trúc hiện tại của Splitly](/images/2-Proposal/Splitly/Architecture_Final.png)

Hệ thống hiện tại được tổ chức theo bốn nhóm thành phần.

### 3.1 Lớp truy cập và mạng

- Tài nguyên được đặt tại Region `ap-southeast-1` để giảm độ trễ khi người dùng truy cập từ Việt Nam.
- EC2 nằm trong public subnet của Amazon VPC và kết nối Internet qua Internet Gateway.
- Security Group chỉ cho phép lưu lượng cần thiết. HTTP cổng 80 phục vụ phiên bản workshop; backend cổng 5000 chỉ lắng nghe nội bộ và không được mở trực tiếp ra Internet.
- Quản trị viên ưu tiên kết nối bằng AWS Systems Manager Session Manager, tránh phụ thuộc vào cổng SSH công khai.
- Elastic IP giúp địa chỉ truy cập không thay đổi khi instance được khởi động lại, nhưng cần được theo dõi vì địa chỉ IPv4 công khai có thể phát sinh chi phí.

### 3.2 Lớp trình bày và ứng dụng

- React/Vite được build thành HTML, CSS và JavaScript trong thư mục `dist` trên EC2.
- Nginx phục vụ các tệp frontend ở cổng 80 và xử lý fallback cho các route của Single Page Application.
- Các request `/api/` được Nginx chuyển tiếp đến Node.js/Express tại `127.0.0.1:5000`.
- PM2 quản lý tiến trình `splitly-api`, hỗ trợ tự khởi động lại và xem log khi ứng dụng gặp lỗi.
- Backend thực hiện xác thực, quản lý nhóm, khoản chi, tính số dư, settlement, biên lai, khiếu nại và thông báo.

### 3.3 Lớp dữ liệu và tích hợp

- MongoDB Atlas lưu người dùng, nhóm, khoản chi, settlement, notification và metadata của biên lai.
- Amazon S3 Receipts Bucket lưu file biên lai; database chỉ giữ object key, URL và thông tin liên quan thay vì lưu file nhị phân.
- Backend kết nối tới Gmail SMTP và VNPay Sandbox qua Internet khi các tích hợp này được bật.
- Tên bucket, Region và thời hạn presigned URL được cung cấp qua biến môi trường của backend.

### 3.4 Bảo mật, giám sát và chi phí

- EC2 sử dụng IAM Role để truy cập đúng S3 bucket và gửi dữ liệu giám sát, không lưu AWS Access Key trong mã nguồn.
- MongoDB URI, JWT secret, Gmail App Password và khóa VNPay không được commit lên Git. Trong workshop chúng được đặt trong `.env`; ở môi trường production nên chuyển sang AWS Secrets Manager hoặc Systems Manager Parameter Store.
- CloudWatch thu thập metric và log cần thiết; alarm có thể chuyển sự kiện sang SNS để gửi email cho quản trị viên.
- AWS Budgets theo dõi chi phí thực tế và dự báo, giúp nhóm phát hiện sớm mức sử dụng vượt kế hoạch.

### 3.5 Vai trò của các dịch vụ AWS

| Dịch vụ | Vai trò trong Splitly |
|---|---|
| Amazon EC2 | Chạy Nginx, frontend đã build và backend Node.js |
| Amazon VPC | Cô lập mạng, quản lý subnet, route và kết nối Internet |
| Security Group | Kiểm soát lưu lượng vào/ra của EC2 |
| Amazon S3 | Lưu biên lai do người dùng tải lên |
| AWS IAM | Cấp quyền tối thiểu cho EC2 truy cập S3 và CloudWatch |
| AWS Systems Manager | Cung cấp kênh quản trị EC2 bằng Session Manager |
| Amazon CloudWatch | Thu thập metric, log và tạo alarm |
| Amazon SNS | Gửi cảnh báo vận hành tới quản trị viên |
| AWS Budgets | Theo dõi và cảnh báo chi phí |

MongoDB Atlas, Gmail và VNPay là dịch vụ bên ngoài AWS nhưng tham gia trực tiếp vào luồng nghiệp vụ.

## 4. Kiến trúc mở rộng được đề xuất

![Kiến trúc mở rộng của Splitly](/images/2-Proposal/Splitly/Architecture_Update.png)

Khi lượng truy cập và yêu cầu bảo mật tăng, frontend nên được tách khỏi EC2:

1. React/Vite được build và đưa vào một S3 Frontend Bucket riêng.
2. CloudFront phân phối nội dung tĩnh qua edge location và cache các tài nguyên phù hợp.
3. Route 53 quản lý tên miền; AWS Certificate Manager cung cấp chứng chỉ TLS cho HTTPS.
4. AWS WAF lọc các request đi qua CloudFront theo rule đã cấu hình.
5. EC2 tiếp tục xử lý REST API, MongoDB Atlas và S3 Receipts Bucket trong giai đoạn chuyển tiếp.

Việc tách frontend mang lại khả năng triển khai độc lập, giảm tải EC2 và cải thiện tốc độ tải trang. Tuy nhiên, để bảo vệ API toàn diện ở giai đoạn production, luồng API cũng cần đi qua một điểm vào được quản lý như CloudFront behavior, Application Load Balancer hoặc API Gateway; chỉ đặt WAF trước đường phân phối frontend không tự động bảo vệ mọi request tới EC2.

Các bước mở rộng tiếp theo có thể bao gồm Auto Scaling, Application Load Balancer, private subnet cho backend, database backup, CI/CD và quản lý secret tập trung. Các hạng mục này chỉ được bổ sung sau khi có số liệu tải và yêu cầu sẵn sàng thực tế.

## 5. Kế hoạch triển khai kỹ thuật

### Giai đoạn 1 – Hoàn thiện yêu cầu và thiết kế

- Chuẩn hóa use case, vai trò người dùng và quy tắc chia tiền.
- Rà soát cấu trúc frontend, backend và schema MongoDB.
- Vẽ kiến trúc hiện tại, xác định trust boundary và luồng dữ liệu nhạy cảm.
- Xác định quy ước tên tài nguyên, Region và chiến lược gắn tag.

### Giai đoạn 2 – Chuẩn bị hạ tầng

- Dùng CloudFormation tạo VPC, subnet, route, Security Group, EC2 và IAM role.
- Tạo S3 Receipts Bucket với public access bị chặn và chính sách phù hợp.
- Chuẩn bị MongoDB Atlas Network Access và tài khoản database có quyền giới hạn.
- Thiết lập CloudWatch, SNS và AWS Budgets theo phạm vi thực hành.

### Giai đoạn 3 – Triển khai ứng dụng

- Kết nối EC2 qua Session Manager và clone repository của nhóm.
- Cấu hình backend bằng biến môi trường; cài dependency, build và chạy bằng PM2.
- Cấu hình frontend production, build React/Vite và kiểm tra `dist/index.html`.
- Cấu hình Nginx để phục vụ frontend và reverse proxy `/api/` tới backend.

### Giai đoạn 4 – Kiểm thử và bàn giao

- Kiểm tra hạ tầng, PM2, cổng backend, Nginx và truy cập từ trình duyệt.
- Kiểm thử các luồng đăng nhập, tạo nhóm, thêm chi phí, tính số dư và upload biên lai.
- Đối chiếu log CloudWatch, lỗi ứng dụng và cảnh báo chi phí.
- Hoàn thiện hướng dẫn vận hành, phương án khôi phục và quy trình dọn dẹp tài nguyên.

## 6. Yêu cầu và tiêu chí nghiệm thu

### 6.1 Yêu cầu kỹ thuật

- Frontend: React, TypeScript, Vite; không chứa secret trong biến `VITE_`.
- Backend: Node.js, Express, TypeScript, REST API; PM2 giữ tiến trình ổn định.
- Web server: Nginx phục vụ SPA và proxy API.
- Dữ liệu: MongoDB Atlas lưu dữ liệu nghiệp vụ; S3 lưu biên lai.
- Bảo mật: IAM Role, Security Group tối thiểu, secret không nằm trong repository.
- Quan sát: có log backend, metric EC2 và kênh cảnh báo quản trị.

### 6.2 Tiêu chí nghiệm thu

- CloudFormation stack tạo thành công và các tài nguyên đạt trạng thái hoạt động.
- Giao diện Splitly truy cập được từ địa chỉ public; refresh route SPA không trả về 404.
- `splitly-api` ở trạng thái `online`; API phản hồi qua Nginx mà không công khai cổng 5000.
- Người dùng có thể tạo nhóm, ghi nhận khoản chi và nhận kết quả số dư đúng với dữ liệu kiểm thử.
- Biên lai được lưu vào đúng S3 bucket và metadata liên kết được với giao dịch.
- Không xuất hiện credential thật trong Git, ảnh báo cáo hoặc log được chia sẻ.
- Nhóm có thể tìm nguyên nhân của một lỗi giả lập thông qua PM2/CloudWatch và nhận cảnh báo đã cấu hình.

## 7. Lộ trình dự kiến

| Thời gian | Mục tiêu chính | Sản phẩm bàn giao |
|---|---|---|
| Tuần 1–2 | Phân tích yêu cầu và thiết kế | Use case, schema dữ liệu, sơ đồ kiến trúc |
| Tuần 3–5 | Hoàn thiện chức năng cốt lõi | Authentication, nhóm, chi phí, settlement, receipt |
| Tuần 6–8 | Xây dựng hạ tầng và triển khai | CloudFormation stack, EC2, S3, ứng dụng hoạt động |
| Tuần 9–10 | Kiểm thử và tăng cường bảo mật | Kết quả test, IAM/SG đã rà soát, log và alarm |
| Tuần 11–12 | Tối ưu, tài liệu và bàn giao | Báo cáo, hướng dẫn vận hành, kế hoạch mở rộng |

Lộ trình có thể điều chỉnh theo tiến độ phát triển phần mềm, nhưng mỗi giai đoạn chỉ hoàn tất khi sản phẩm bàn giao tương ứng đã được kiểm chứng.

## 8. Ước tính và kiểm soát chi phí

Chi phí không nên được sao chép cố định từ một bài mẫu vì phụ thuộc thời điểm, Region, loại tài khoản, thời gian chạy EC2, dung lượng S3, log và lưu lượng Internet. Trước khi triển khai, nhóm cần tạo một estimate mới trên AWS Pricing Calculator với giả định thực tế.

Các nguồn chi phí chính:

- Thời gian chạy và loại instance EC2.
- Địa chỉ public IPv4/Elastic IP.
- Dung lượng, request và data transfer của S3.
- Dung lượng CloudWatch Logs, metric tùy chỉnh và alarm.
- Data transfer ra Internet; chi phí MongoDB Atlas nằm ngoài hóa đơn AWS.

Biện pháp kiểm soát gồm gắn tag cho tài nguyên, thiết lập AWS Budgets, giới hạn thời gian giữ log, xóa tài nguyên lab sau khi dùng, kiểm tra S3 lifecycle và dừng/xóa EC2 không còn cần thiết. Báo cáo chi phí cuối cùng phải ghi rõ ngày ước tính và các giả định tải.

## 9. Rủi ro và phương án ứng phó

| Rủi ro | Mức ảnh hưởng | Giảm thiểu và dự phòng |
|---|---|---|
| EC2 hoặc tiến trình backend ngừng hoạt động | Cao | PM2 tự khởi động lại, CloudWatch alarm; redeploy từ repository và CloudFormation |
| Mất kết nối MongoDB Atlas | Cao | Giới hạn tài khoản DB, kiểm tra allowlist, theo dõi log; sử dụng backup của Atlas khi cần |
| Upload/đọc biên lai thất bại | Trung bình | IAM tối thiểu, kiểm tra Region/bucket, retry hợp lý; giữ metadata để đối soát |
| Lộ secret trong Git hoặc log | Cao | `.gitignore`, rà soát trước commit, xoay vòng credential và chuyển sang secret store khi mở rộng |
| Security Group cấu hình quá rộng | Cao | Không mở cổng 5000; ưu tiên Session Manager; rà soát rule định kỳ |
| Sai kết quả chia tiền | Cao | Unit test cho quy tắc làm tròn/chia, bộ dữ liệu đối chiếu và audit lịch sử chỉnh sửa |
| Chi phí vượt dự kiến | Trung bình | AWS Budgets, tag, cảnh báo sớm và dọn tài nguyên không sử dụng |
| Kiến trúc một EC2 tạo điểm lỗi đơn | Cao | Chấp nhận trong giai đoạn lab; sao lưu cấu hình và chuẩn bị lộ trình ALB/Auto Scaling |

## 10. Kết quả mong đợi

- Splitly vận hành ổn định trên AWS với luồng frontend, API, database và biên lai hoạt động xuyên suốt.
- Thành viên quản lý chi phí minh bạch hơn, giảm thời gian tính toán và đối soát thủ công.
- Nhóm áp dụng được IAM Role, phân tách file và metadata, giám sát tập trung và cảnh báo ngân sách.
- Hạ tầng có thể tái tạo bằng CloudFormation và có tài liệu triển khai, kiểm thử, khắc phục sự cố, dọn dẹp.
- Kiến trúc hiện tại tạo nền tảng rõ ràng cho việc tách frontend, bổ sung HTTPS, tên miền, WAF, cân bằng tải và CI/CD trong giai đoạn sau.
