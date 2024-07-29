An IAM role is an identity that can be assumed by someone or something who needs temporary access to AWS credentials.

The important thing to know about roles is that the credentials they provide expire and roles are assumed programmatically.

IAM roles are identities in AWS that like an IAM user also have associated AWS credentials used to sign requests. However, IAM users have usernames and passwords as well as static credentials whereas IAM roles do not have any login credentials like a username and password and the credentials used to sign requests are programmatically acquired, temporary in nature, and automatically rotated. 

Maintaining roles is more efficient than maintaining users. When you assume a role, IAM dynamically provides temporary credentials that expire after a defined period of time, between 15 minutes and 36 hours. Users, on the other hand, have long-term credentials in the form of user name and password combinations or a set of access keys.

User access keys only expire when you or the account admin rotates the keys. User login credentials expire if you applied a password policy to your account that forces users to rotate their passwords.

Roles are normally used for AWS services to communicate to other services. The credentials for the roles can be retrieved programmatically when assigned to an AWS instance by the app running on the instance. 