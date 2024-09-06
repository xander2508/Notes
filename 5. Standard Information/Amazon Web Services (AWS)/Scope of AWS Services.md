---
tags:
  - AWS
  - AmazonWebServices
  - StandardInformation
---
Depending on the AWS service that you use, your resources are either deployed at the [[Availability Zones|Availability Zone]], [[Regions|Region]], or Global level. Each service is different, so you must understand how the scope of a service might affect your application architecture.  
  
When you operate a Region-scoped service, you only need to select the Region that you want to use. If you are not asked to specify an individual Availability Zone to deploy the service in, this is an indicator that the service operates on a Region-scope level. For Region-scoped services, AWS automatically performs actions to increase data durability and availability.  
  
On the other hand, some services ask you to specify an Availability Zone. With these services, you are often responsible for increasing the data durability and high availability of these resources.