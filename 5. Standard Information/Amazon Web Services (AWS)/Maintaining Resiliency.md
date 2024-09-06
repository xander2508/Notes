---
tags:
  - AWS
  - AmazonWebServices
  - StandardInformation
---
To keep your application available, you must maintain high availability and resiliency. A well-known best practice for cloud architecture is to use Region-scoped, managed services. These services come with availability and resiliency built in. When that is not possible, make sure your workload is replicated across multiple [[Availability Zones]]. At a minimum, you should use two [[Availability Zones]]. That way, if an Availability Zone fails, your application will have infrastructure up and running in a second Availability Zone to take over the traffic.