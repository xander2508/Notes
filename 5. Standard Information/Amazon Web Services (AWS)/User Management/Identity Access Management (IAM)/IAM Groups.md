---
tags:
  - AWS
  - AmazonWebServices
  - UserManagement
  - IdentityAccessManagement
  - IAM
---
An IAM group is a collection of users. All users in the group inherit the permissions assigned to the group. This makes it possible to give permissions to multiple users at once. It’s a more convenient and scalable way of managing permissions for users in your AWS account. This is why using IAM groups is a best practice.

![[Pasted image 20240729101715.png]]

Keep in mind the following features of groups:

- Groups can have many users.
- Users can belong to many groups.
- Groups cannot belong to groups.

Groups have [[IAM Policies]] attached to them which handle the permissions. 