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
| Thứ Hai | Kiểm tra CloudFormation output, trạng thái EC2, rule Security Group, IAM Role, Session Manager và các cổng cần lắng nghe. | 03/08/2026 | 03/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> <https://000037.awsstudygroup.com/> |
| Thứ Ba | Kiểm tra backend health, log PM2, cấu hình Nginx, refresh route SPA và luồng frontend tới API. | 04/08/2026 | 04/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Thứ Tư | Kiểm thử đăng nhập, tạo nhóm, khoản chi, số dư, settlement, upload/đọc biên lai, notification và complaint. | 05/08/2026 | 05/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> [../../2-proposal/](../../2-proposal/) |
| Thứ Năm | Rà soát log/metric CloudWatch, cảnh báo SNS, AWS Budgets, phạm vi IAM/Security Group và các tình huống xử lý lỗi. | 06/08/2026 | 06/08/2026 | <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Thứ Sáu | Hoàn thiện tài liệu Anh/Việt, sao lưu bằng chứng cần thiết, dọn tài nguyên lab an toàn và rà soát báo cáo. | 07/08/2026 | 07/08/2026 | [../../5-workshop/5.5-cleanup/](../../5-workshop/5.5-cleanup/) <br> <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 12:

* Kiểm tra độc lập các lớp hạ tầng, backend, frontend, proxy, database và receipt storage.
* Xác nhận các luồng nghiệp vụ chính của Splitly bằng bộ dữ liệu chuẩn bị trước.
* Ghi lại ma trận xử lý lỗi dựa trên triệu chứng quan sát được và log.
* Rà soát kiểm soát bảo mật, chi phí và xóa an toàn tài nguyên tính phí của workshop.
* Hoàn thành Proposal, workshop triển khai Splitly và Worklog 12 tuần để rà soát lần cuối trước ngày 09/08/2026.
