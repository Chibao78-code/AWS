+++
title = "Clean up"
date = 2026-08-06
weight = 5
chapter = false
pre = "<b>5.5. </b>"
+++

# CLEAN UP RESOURCES

Remove resources that are no longer required after the workshop to prevent unnecessary charges.

## 1. Determine deletion scope

CloudFormation deletes only resources managed by the stack. Review **Resources** and **Outputs** before deletion to distinguish stack resources from manually created or shared assets.

If a stack-owned S3 bucket contains receipts, back up anything that must be retained and empty the bucket first. A non-empty bucket can cause stack deletion to fail. Never delete production or shared team data.

## 2. Delete the stack

1. Open **CloudFormation** and select the Splitly stack.
2. Choose **Delete** and confirm.

   ![Delete stack](/images/5-Workshop/Splitly/5.5-Cleanup/1.png)

3. Monitor **Events** until the stack disappears or reaches `DELETE_COMPLETE`.

   ![Monitor deletion](/images/5-Workshop/Splitly/5.5-Cleanup/2.png)

For `DELETE_FAILED`, inspect the failed resource event, resolve that specific dependency, and retry. Common causes include a non-empty bucket or deletion protection.

## 3. Review resources outside the stack

Check for:

- Manually created S3 objects/buckets, CloudWatch log groups, and alarms.
- Elastic IPs, snapshots, EBS volumes, or Security Groups not managed by the stack.
- Test data in MongoDB Atlas.
- Gmail App Passwords, deploy keys, and temporary credentials used for the workshop.
- Google OAuth or VNPay Sandbox settings that are no longer needed.

Cleanup is complete when no workshop-specific EC2, Elastic IP, or other billable resource remains and any required data has been backed up safely.
