Amazon EC2 is a web service that provides secure, resizable compute capacity in the cloud. With this service, you can provision virtual servers called EC2 instances.

With Amazon EC2, you can do the following:

- Provision and launch one or more EC2 instances in minutes.
- Stop or shut down EC2 instances when you finish running a workload.
- Pay by the hour or second for each instance type (minimum of 60 seconds).

To create an EC2 instance, you must define the following:
- **Hardware specifications:** CPU, memory, network, and storage
- **Logical configurations:** Networking location, firewall rules, authentication, and the operating system of your choice

# Amazon Machine Image 

When launching an EC2 instance, the first setting you configure is which operating system you want by selecting an Amazon Machine Image (AMI).

In the AWS Cloud, the operating system installation is not your responsibility. Instead, it's built into the AMI that you choose.

An AMI includes the operating system, storage mapping, architecture type, launch permissions, and any additional preinstalled software applications.

One advantage of using AMIs is that they are reusable. You could create an AMI from your running instance and use the AMI to start a new instance. That way, your new instance would have the same configurations as your current instance because the configurations set in the AMIs are the same.

![[Pasted image 20240729114812.png]]

| Finding AMIs         |                                                                                                    |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| Quick Start AMIs     | Quick Start AMIs are commonly used AMIs created by AWS that you can select to get started quickly. |
| AWS Marketplace AMIs | AWS Marketplace AMIs provide popular open-source and commercial software from third-party vendors. |
| My AMIs              | My AMIs are created from your EC2 instances.                                                       |
| Community AMIs       | Community AMIs are provided by the AWS user community.                                             |
| Custom image         | Build your own custom image with EC2 Image Builder.                                                |
Each AMI in the AWS Management Console has an AMI ID, which is prefixed by _ami-_, followed by a random hash of numbers and letters. The IDs are unique to each AWS Region.