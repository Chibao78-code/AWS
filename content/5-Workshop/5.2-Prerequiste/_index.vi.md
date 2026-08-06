+++
title = "Prerequiste"
date = 2026-08-06
weight = 2
chapter = false
pre = "<b>5.2. </b>"
+++

# CHUẨN BỊ MÔI TRƯỜNG

## 1. Thông tin cần có

Trước khi tạo hạ tầng, chuẩn bị:

- Tài khoản AWS và Region thống nhất của nhóm, ví dụ `ap-southeast-1`.
- Tệp CloudFormation YAML của dự án Splitly.
- URL repository Git chứa hai thư mục `app` và `backend`.
- Chuỗi kết nối MongoDB Atlas và database `Splitly`; Network Access của Atlas phải cho phép EC2 kết nối.
- Gmail App Password và Google Client ID nếu kiểm thử đăng nhập/gửi email.
- Tên S3 bucket lưu hóa đơn. Tên bucket phải duy nhất trên toàn AWS.
- Thông tin VNPay Sandbox nếu kiểm thử thanh toán; có thể để trống trong bài thực hành cơ bản.

{{% notice warning %}}
Không ghi mật khẩu, JWT secret hoặc URI MongoDB thật vào tài liệu và repository. Với môi trường thật, nên lưu bí mật trong AWS Secrets Manager hoặc Systems Manager Parameter Store.
{{% /notice %}}

## 2. Quyền IAM cho người triển khai

Tài khoản thực hành cần quyền tạo CloudFormation stack, EC2, S3, CloudWatch và IAM role cho EC2. Chính sách sau phản ánh phạm vi của bài lab và sử dụng quyền khá rộng để giảm lỗi trong lớp học:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:*",
        "ec2:*",
        "s3:*",
        "cloudwatch:*",
        "logs:*",
        "sns:*"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "iam:DeleteRole",
        "iam:GetRole",
        "iam:CreateInstanceProfile",
        "iam:DeleteInstanceProfile",
        "iam:AddRoleToInstanceProfile",
        "iam:RemoveRoleFromInstanceProfile",
        "iam:AttachRolePolicy",
        "iam:DetachRolePolicy",
        "iam:PutRolePolicy",
        "iam:DeleteRolePolicy",
        "iam:TagRole"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": "ec2.amazonaws.com"
        }
      }
    }
  ]
}
```

<!-- {{% notice note %}}
Chính sách trên chỉ phù hợp với tài khoản lab. Trong môi trường thật, hãy giới hạn `Action` và `Resource` theo nguyên tắc đặc quyền tối thiểu, đồng thời dùng role tạm thời thay cho access key dài hạn.
{{% /notice %}} -->

## 3. Tạo hạ tầng bằng CloudFormation

1. Mở **AWS Management Console**, tìm **CloudFormation** và chọn **Create stack → With new resources (standard)**.

   ![Mở CloudFormation](/images/5-Workshop/Splitly/5.2-Prerequisite/1.png)

2. Chọn **Upload a template file**, tải tệp YAML của nhóm lên rồi chọn **Next**.

   ![Tải CloudFormation template](/images/5-Workshop/Splitly/5.2-Prerequisite/2.png)

3. Đặt tên stack dễ nhận biết, chẳng hạn `splitly-workshop`, và nhập các parameter theo template: VPC CIDR, subnet, instance type, bucket name hoặc key pair nếu template yêu cầu.

   ![Cấu hình stack](/images/5-Workshop/Splitly/5.2-Prerequisite/3.png)

4. Kiểm tra cấu hình stack, thẻ tài nguyên và quyền IAM.

   ![Kiểm tra cấu hình](/images/5-Workshop/Splitly/5.2-Prerequisite/4.png)

5. Đánh dấu xác nhận CloudFormation có thể tạo IAM resources, sau đó chọn **Submit**.

   ![Xác nhận quyền IAM](/images/5-Workshop/Splitly/5.2-Prerequisite/5.png)

6. Theo dõi tab **Events** đến khi stack chuyển sang `CREATE_COMPLETE`. Nếu thất bại, mở event đầu tiên có trạng thái `CREATE_FAILED` để xem nguyên nhân gốc.

   ![Theo dõi quá trình tạo](/images/5-Workshop/Splitly/5.2-Prerequisite/6.png)

7. Kiểm tra tab **Resources** và **Outputs** để lấy EC2 Instance ID, Public IP, tên bucket và các giá trị đầu ra khác.

   ![Kiểm tra tài nguyên](/images/5-Workshop/Splitly/5.2-Prerequisite/7.png)

   ![Kiểm tra output](/images/5-Workshop/Splitly/5.2-Prerequisite/8.png)

## 4. Kiểm tra trước khi triển khai mã nguồn

- EC2 có trạng thái `Running` và vượt qua toàn bộ status checks.
- Instance xuất hiện trong **Systems Manager → Fleet Manager/Managed nodes** hoặc có thể chọn **Session Manager** từ màn hình Connect.
- Security Group cho phép HTTP cổng 80 từ địa chỉ cần kiểm thử; không cần mở cổng 5000 ra Internet vì Nginx gọi backend nội bộ.
- IAM role gắn với EC2 có quyền cần thiết với đúng S3 bucket và CloudWatch.
- MongoDB Atlas cho phép kết nối từ địa chỉ mạng của EC2.

![Kiểm tra EC2](/images/5-Workshop/Splitly/5.2-Prerequisite/10.png)

![Kiểm tra Session Manager](/images/5-Workshop/Splitly/5.2-Prerequisite/11.png)
