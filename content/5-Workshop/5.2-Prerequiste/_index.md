+++
title = "Prerequiste"
date = 2026-08-06
weight = 2
chapter = false
pre = "<b>5.2. </b>"
+++

# PREPARE THE ENVIRONMENT

## 1. Required information

Before provisioning infrastructure, prepare:

- An AWS account and a team-wide Region, such as `ap-southeast-1`.
- The Splitly CloudFormation YAML template.
- The Git repository URL containing the `app` and `backend` directories.
- A MongoDB Atlas connection string and the `Splitly` database; Atlas Network Access must permit the EC2 connection.
- A Gmail App Password and Google Client ID when email and Google sign-in are tested.
- A globally unique S3 bucket name for receipt images.
- VNPay Sandbox credentials only when the payment integration is in scope.

{{% notice warning %}}
Do not place real passwords, JWT secrets, or MongoDB URIs in this report or repository. For a production environment, use AWS Secrets Manager or Systems Manager Parameter Store.
{{% /notice %}}

## 2. Deployment permissions

The lab identity needs permission to operate CloudFormation, EC2, S3, CloudWatch, and the EC2 IAM role. The following deliberately broad policy reflects a short-lived lab environment:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:*", "ec2:*", "s3:*",
        "cloudwatch:*", "logs:*", "sns:*"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole", "iam:DeleteRole", "iam:GetRole",
        "iam:CreateInstanceProfile", "iam:DeleteInstanceProfile",
        "iam:AddRoleToInstanceProfile", "iam:RemoveRoleFromInstanceProfile",
        "iam:AttachRolePolicy", "iam:DetachRolePolicy",
        "iam:PutRolePolicy", "iam:DeleteRolePolicy", "iam:TagRole"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "*",
      "Condition": {
        "StringEquals": { "iam:PassedToService": "ec2.amazonaws.com" }
      }
    }
  ]
}
```

<!-- {{% notice note %}}
Use this policy only in a lab account. Production permissions should restrict both actions and resources according to least privilege and should favor temporary roles over long-lived access keys.
{{% /notice %}} -->

## 3. Provision with CloudFormation

1. Open **CloudFormation** and select **Create stack → With new resources (standard)**.

   ![Open CloudFormation](/images/5-Workshop/Splitly/5.2-Prerequisite/1.png)

2. Select **Upload a template file**, upload the team's YAML template, and choose **Next**.

   ![Upload template](/images/5-Workshop/Splitly/5.2-Prerequisite/2.png)

3. Enter a recognizable name such as `splitly-workshop` and supply the parameters requested by the template.

   ![Configure stack](/images/5-Workshop/Splitly/5.2-Prerequisite/3.png)

4. Review stack options, tags, and IAM permissions.

   ![Review configuration](/images/5-Workshop/Splitly/5.2-Prerequisite/4.png)

5. Acknowledge that CloudFormation may create IAM resources and select **Submit**.

   ![Acknowledge IAM resources](/images/5-Workshop/Splitly/5.2-Prerequisite/5.png)

6. Monitor **Events** until the stack reaches `CREATE_COMPLETE`. If it fails, inspect the earliest `CREATE_FAILED` event for the root cause.

   ![Monitor stack creation](/images/5-Workshop/Splitly/5.2-Prerequisite/6.png)

7. Review **Resources** and **Outputs** for the EC2 instance ID, public IP, bucket name, and other generated values.

   ![Review resources](/images/5-Workshop/Splitly/5.2-Prerequisite/7.png)

   ![Review outputs](/images/5-Workshop/Splitly/5.2-Prerequisite/8.png)

## 4. Pre-deployment checks

- EC2 is `Running` and all status checks pass.
- The instance can be reached through Session Manager.
- The Security Group permits HTTP port 80 from the intended test source. Port 5000 stays private.
- The attached EC2 role grants only the required access to the receipt bucket and CloudWatch.
- MongoDB Atlas allows the EC2 network to connect.

![Check EC2](/images/5-Workshop/Splitly/5.2-Prerequisite/10.png)

![Check Session Manager](/images/5-Workshop/Splitly/5.2-Prerequisite/11.png)
