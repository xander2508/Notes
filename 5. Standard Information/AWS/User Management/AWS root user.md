When you first create an AWS account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS root user and is accessed by signing in with the email address and password that were used to create the account.

### AWS root user credentials

The AWS root user has two sets of credentials associated with it. One set of credentials is the email address and password that were used to create the account. This allows you to access the AWS Management Console. The second set of credentials is called access keys, which allow you to make programmatic requests from the AWS Command Line Interface (AWS CLI) or AWS API.  
  
Access keys consist of two parts:

- **Access key ID:** for example,`A2lAl5EXAMPLE`
- **Secret access key:** for example, `wJalrFE/KbEKxE`


> [!NOTE] **Delete your access keys to stay safe!**
> If you don't have an access key for your AWS account root user, don't create one unless you absolutely need to. If you have an access key for your AWS account root user and want to delete the key, follow these steps:
> 
> 1. In the AWS Management Console, navigate to your username in the upper right section of the navigation bar. From the dropdown menu, go to the **My Security Credentials** page, and sign in with the root user’s email address and password.
> 2. Open the **Access keys** section.
> 3. Under **Actions**, choose **Delete**.
> 4. Choose **Yes**.


### AWS root user best practices

The root user has complete access to all AWS services and resources in your account, including your billing and personal information. Therefore, you should securely lock away the credentials associated with the root user and not use the root user for everyday tasks. Visit the links at the end of this lesson to learn more about when to use the AWS root user.

To ensure the safety of the root user, follow these best practices:

- Choose a strong password for the root user.
- Enable [[multi-factor authentication (MFA)]] for the root user.
- Never share your root user password or access keys with anyone.
- Disable or delete the access keys associated with the root user.
- Create an [[Identity and Access Management (IAM)]] user for administrative tasks or everyday tasks.