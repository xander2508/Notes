---
tags:
  - AWS
  - AmazonWebServices
  - Services
  - StandardInformation
---
[AWS Command Line Interface](https://aws.amazon.com/cli/)

The AWS CLI is a unified tool that you can use to manage AWS services. You can download and configure one tool that you can use to control multiple AWS services from the command line, and automate them with scripts. 

The AWS CLI is open source, and installers are available for Windows, Linux, and macOS.

Consider the scenario where you run many servers on AWS for your application’s frontend. You want to run a report to collect data from all the servers. You need to do this programmatically every day because the server details might change. Instead of manually logging in to the console and then copying and pasting information, you can schedule an AWS CLI script with an API call to pull this data for you.

For example, you run the following API call against a service, using the AWS CLI:  
```
aws s3api list-buckets
```

You will get a response similar to the following one, listing the buckets in your AWS accounts:

```
{
    "Owner": {
        "DisplayName": "tech-essentials", 
        "ID": "d9881f40b83adh2896eb276f44ffch53677faec805422c83dfk60cc335a7da92"
    }, 
    "Buckets": [
        {
            "CreationDate": "2023-01-10T15:50:20.000Z", 
            "Name": "aws-tech-essentials"
        }, 
        {
            "CreationDate": "2023-01-10T16:04:15.000Z", 
            "Name": "aws-tech-essentials-employee-directory-app"
        } 
    ]
}
```

