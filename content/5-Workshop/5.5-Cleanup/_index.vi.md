+++
title = "Dọn dẹp tài nguyên"
date = 2026-07-16
weight = 5
chapter = false
pre = "<b>5.5. </b>"
+++

# DỌN DẸP TÀI NGUYÊN

Sau khi hoàn thành workshop, xóa tài nguyên không còn sử dụng để tránh phát sinh chi phí.

## 1. Xác định phạm vi cần xóa

CloudFormation chỉ xóa những tài nguyên do stack quản lý. Trước khi thực hiện, kiểm tra tab **Resources** và **Outputs** để phân biệt tài nguyên thuộc stack với tài nguyên được tạo thủ công.

Nếu S3 bucket nằm trong stack và đang chứa ảnh hóa đơn, hãy sao lưu dữ liệu cần giữ rồi xóa object; bucket không rỗng có thể làm stack xóa thất bại. Không xóa dữ liệu production hoặc tài nguyên dùng chung của nhóm.

## 2. Xóa CloudFormation stack

1. Mở **CloudFormation**, chọn stack Splitly.
2. Chọn **Delete** và xác nhận.

   ![Chọn xóa stack](/images/5-Workshop/Splitly/5.5-Cleanup/1.png)

3. Theo dõi tab **Events** đến khi stack biến mất hoặc đạt `DELETE_COMPLETE`.

   ![Theo dõi quá trình xóa](/images/5-Workshop/Splitly/5.5-Cleanup/2.png)

Nếu gặp `DELETE_FAILED`, đọc thông báo của tài nguyên thất bại, xử lý đúng tài nguyên đó rồi thử lại; nguyên nhân thường gặp là S3 bucket còn object hoặc tài nguyên có deletion protection.

## 3. Kiểm tra tài nguyên ngoài stack

Sau khi stack được xóa, rà soát:

- S3 bucket/object, CloudWatch Log Group và alarm được tạo thủ công.
- Elastic IP, snapshot, volume EBS hoặc Security Group không thuộc stack.
- Dữ liệu thử nghiệm trong MongoDB Atlas.
- Gmail App Password, deploy key hoặc thông tin xác thực tạm thời đã dùng trong buổi thực hành.
- Cấu hình Google OAuth/VNPay Sandbox không còn cần thiết.

Kết thúc dọn dẹp khi không còn EC2, Elastic IP hay tài nguyên tính phí dành riêng cho workshop và dữ liệu cần giữ đã được sao lưu an toàn.
