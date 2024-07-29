#### Lock down the AWS root user

The [[AWS root user]] is an all-powerful and all-knowing identity in your AWS account. If a malicious user were to gain control of root-user credentials, they would be able to access every resource in your account, including personal and billing information. To lock down the root user, you can do the following:

- Don’t share the credentials associated with the root user.
- Consider deleting the root user access keys.
- Activate MFA on the root account.


#### Follow the principle of least privilege

Least privilege is a standard security principle that advises you to grant only the necessary permissions to do a particular job and nothing more. To implement least privilege for access control, start with the minimum set of permissions in an IAM policy and then grant additional permissions as necessary for a user, group, or role.