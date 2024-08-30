---
tags:
  - AWS
  - AmazonWebServices
  - UserManagement
  - IdentityAccessManagement
  - IAM
---
An IAM user represents a person or service that interacts with AWS. You define the user in your AWS account. Any activity done by that user is billed to your account. When you create a user, that user can sign in to gain access to the AWS resources inside your account.

You can also add more users to your account as needed. Each person should have their own login credentials to prevent sharing credentials between users.
### IAM user credentials

An IAM user consists of a name and a set of credentials. When you create a user, you can provide them with the following types of access:

- Access to the AWS Management Console
- Programmatic access to the AWS CLI and AWS API

To access the console, provide the user with a user name and password. For programmatic access, AWS generates a set of access keys that can be used with the AWS CLI and AWS API. IAM user credentials are considered permanent, which means that they stay with the user until there’s a forced rotation by admins.

Fortunately, you can group IAM users and attach permissions at the group level. [[IAM Groups]] should be used to assign permissions. 

To allow an IAM identity to perform specific actions in AWS, such as implement resources, you must grant the IAM user the necessary permissions.