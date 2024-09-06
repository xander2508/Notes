---
tags:
  - AWS
  - AmazonWebServices
  - Services
  - Storage
  - BlockStorage
  - StandardInformation
---

[Amazon EC2 Instance Store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)

[[Amazon Elastic Compute Cloud (EC2)]] instance store provides temporary block-level storage for an instance. This storage is located on disks that are physically attached to the host computer. 

This ties the lifecycle of the data to the lifecycle of the EC2 instance. If you delete the instance, the instance store is also deleted. Because of this, instance store is considered ephemeral storage.

It’s ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content.

It can survive a reboot but nothing else.