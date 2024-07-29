To manage access and provide permissions to AWS services and resources, you create IAM policies and attach them to an IAM identity.

Whenever an IAM identity makes a request, AWS evaluates the policies associated with them. For example, if you have a developer inside the developers group who makes a request to an AWS service, AWS evaluates any policies attached to the developers group and any policies attached to the developer user to determine if the request should be allowed or denied.

### IAM policy examples

Most policies are stored in AWS as JSON documents with several policy elements. The following example provides admin access through an IAM identity-based policy.

```json
{
	"Version": "2012-10-17",
	"Statement": [{
		"Effect": "Allow",
		"Action": "*",
		"Resource": "*"
	}]
}
```

This policy has four major JSON elements: _**Version**_, _**Effect**_, _**Action**_, and _**Resource**_.

- The _**Version**_ element defines the version of the policy language. It specifies the language syntax rules that are needed by AWS to process a policy. To use all the available policy features, include **"Version": "2012-10-17"** before the **"Statement"** element in your policies.
- The _**Effect**_ element specifies whether the policy will allow or deny access. In this policy, the Effect is **"Allow"**, which means you’re providing access to a particular resource.
- The _**Action**_ element describes the type of action that should be allowed or denied. In the example policy, the action is **"*"**. This is called a wildcard, and it is used to symbolize every action inside your AWS account.
- The _**Resource**_ element specifies the object or objects that the policy statement covers. In the policy example, the resource is the wildcard **"*"**. This represents all resources inside your AWS console.

Putting this information together, you have a policy that allows you to perform all actions on all resources in your AWS account. This is what we refer to as an administrator policy.  
  
The next example shows a more granular IAM policy.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyS3AccessOutsideMyBoundary",
      "Effect": "Deny",
      "Action": [
        "s3:*"
      ],
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:ResourceAccount": [
            "222222222222"
          ]
        }
      }
    }
  ]
}
```

This policy uses a _Deny_ effect to block access to Amazon S3 actions, unless the Amazon S3 resource that's being accessed is in account _222222222222_. This ensures that any Amazon S3 principals are accessing only the resources that are inside of a trusted AWS account.