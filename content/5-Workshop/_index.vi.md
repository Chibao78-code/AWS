+++
title = "Workshop"
date = 2026-07-16
weight = 5
chapter = false
pre = "<b>5. </b>"
+++

# TRIỂN KHAI ỨNG DỤNG SPLITLY TRÊN AWS

Workshop này trình bày toàn bộ quá trình đưa **Splitly** — ứng dụng quản lý và chia sẻ chi phí nhóm — lên AWS. Hạ tầng nền tảng được khởi tạo bằng AWS CloudFormation; mã nguồn frontend và backend được triển khai trên Amazon EC2; Amazon S3 lưu ảnh hóa đơn; Amazon CloudWatch hỗ trợ theo dõi hệ thống.

Sau khi hoàn thành, bạn có thể:

- Hiểu luồng xử lý từ trình duyệt đến frontend, API và các dịch vụ dữ liệu.
- Tạo nhất quán các tài nguyên mạng, bảo mật và máy chủ bằng CloudFormation.
- Cấu hình biến môi trường mà không đưa khóa bí mật vào mã nguồn.
- Build React/Vite, vận hành Node.js/Express bằng PM2 và cấu hình Nginx reverse proxy.
- Kiểm tra từng lớp của hệ thống, xử lý lỗi phổ biến và dọn dẹp tài nguyên sau thực hành.

Workshop gồm các phần:

1. [Tổng quan workshop](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường](5.2-Prerequiste/)
3. [Triển khai mã nguồn và web server](5.3-DeployCode-WebServer/)
4. [Kiểm thử hệ thống](5.4-Test/)
5. [Dọn dẹp tài nguyên](5.5-Cleanup/)

<!-- {{% notice warning %}}
Các tên tài nguyên, URL repository, địa chỉ IP, chuỗi kết nối và thông tin xác thực trong hướng dẫn chỉ là chỗ giữ chỗ. Hãy thay bằng giá trị của nhóm Splitly và tuyệt đối không commit bí mật lên Git.
{{% /notice %}} -->
