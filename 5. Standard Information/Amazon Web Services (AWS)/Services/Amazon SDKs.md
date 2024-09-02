---
tags:
  - AWS
  - AmazonWebServices
  - Services
---
[Amazon SDKs](https://aws.amazon.com/developer/tools/)

API calls to AWS can be performed by running code with programming languages. You can do this by using AWS SDKs. SDKs are open source and maintained by AWS for the most popular programming languages, such as C++, Go, Java, JavaScript, .NET, Node.js, PHP, Python, Ruby, Rust, and Swift.

Developers commonly use AWS SDKs to integrate their application source code with AWS services.

For example, consider an application with a frontend that runs in Python. Every time the application receives a photo, it uploads the file to a storage service. This action can be achieved in the source code by using the AWS SDK for Python (Boto3). Here is an example of code that you can implement to work with AWS resources using the SDK for Python.

```Python
import boto3
ec2 = boto3.client('ec2')
response = ec2.describe_instances()
print(response)
```