---
title: "Nhật ký công việc tuần 12"
date: 2026-08-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

* Kiểm chứng Splitly theo từng lớp và xử lý lỗi triển khai có hệ thống.
* Hoàn thiện hướng dẫn monitoring, bảo mật, chi phí, dọn dẹp và vận hành.
* Hoàn tất workshop song ngữ và báo cáo thực tập.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ Hai | Đối chiếu output của stack với EC2 đang chạy thật.<br>Xác nhận Security Group chỉ mở đúng cổng cần thiết, không hơn.<br>Session Manager vẫn hoạt động tốt, không cần public SSH key. | 03/08/2026 | 03/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> <https://000037.awsstudygroup.com/> |
| Thứ Ba | Gọi thử endpoint health nhỏ, API phản hồi ổn.<br>Lướt qua log PM2 xem có gì bất thường lúc khởi động không, sạch.<br>Refresh một route sâu của SPA trên trình duyệt để chắc fallback Nginx hoạt động. | 04/08/2026 | 04/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Thứ Tư | Chạy full hành trình bằng tài khoản test: đăng nhập, tạo nhóm, thêm khoản chi.<br>Số dư và settlement khớp với con số mình đã tính trước trên giấy.<br>Upload/tải lại một biên lai, bắn thử một notification và một complaint để kiểm tra cả hai. | 05/08/2026 | 05/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | So metric CloudWatch với mức CPU/network dự kiến thô ban đầu.<br>Gửi thử một alert SNS, nhận được email nên phần này ổn.<br>Viết bảng ngắn triệu chứng thường gặp -> nguyên nhân khả năng cao cho báo cáo. | 06/08/2026 | 06/08/2026 | <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Thứ Sáu | Chụp ảnh minh chứng cuối cho bản chạy thật ở cả hai ngôn ngữ.<br>Sao lưu template CloudFormation và ghi chú cấu hình của mình.<br>Xóa stack + EIP/S3 test còn sót, sau đó đọc lại toàn bộ báo cáo. | 07/08/2026 | 07/08/2026 | [../../5-workshop/5.5-cleanup/](../../5-workshop/5.5-cleanup/) <br> <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 12:

* Kiểm tra độc lập các lớp hạ tầng, backend, frontend, proxy, database và receipt storage.
* Xác nhận các luồng nghiệp vụ chính của Splitly bằng bộ dữ liệu chuẩn bị trước.
* Ghi lại ma trận xử lý lỗi dựa trên triệu chứng quan sát được và log.
* Rà soát kiểm soát bảo mật, chi phí và xóa an toàn tài nguyên tính phí của workshop.
* Hoàn thành Proposal, workshop triển khai Splitly và Worklog 12 tuần để rà soát lần cuối trước ngày 09/08/2026.
