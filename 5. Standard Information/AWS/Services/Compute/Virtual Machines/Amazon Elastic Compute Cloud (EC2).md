[Amazon EC2](https://aws.amazon.com/ec2/)
[What Is EC2 Image Builder?](https://docs.aws.amazon.com/imagebuilder/latest/userguide/what-is-image-builder.html)

Amazon EC2 is a web service that provides secure, resizable compute capacity in the cloud. With this service, you can provision virtual servers called EC2 instances.

You can provision one or many instances easily and at the end of the billing cycle, you only pay for what you use, either per second or per hour depending on the type of the instance. When you no longer need an instance, you can terminate or stop the instance and you will stop incurring charges.

With Amazon EC2, you can do the following:

- Provision and launch one or more EC2 instances in minutes.
- Stop or shut down EC2 instances when you finish running a workload.
- Pay by the hour or second for each instance type (minimum of 60 seconds).

To create an EC2 instance, you must define the following:
- **Hardware specifications:** CPU, memory, network, and storage
- **Logical configurations:** Networking location, firewall rules, authentication, and the operating system of your choice

# Amazon Machine Image 

[Amazon Machine Images (AMI)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
[Creatie an Amazon EBS-Backed Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html)

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
Each AMI in the AWS Management Console has an AMI ID, which is prefixed by `ami-`, followed by a random hash of numbers and letters. The IDs are unique to each AWS Region.

## Amazon EC2 instance types

EC2 instances are a combination of virtual processors (vCPUs), memory, network, and, in some cases, instance storage and graphics processing units (GPUs). When you create an EC2 instance, you need to choose how much you need of each of these components.

Instance types consist of a prefix identifying the type of workloads they’re optimized for, followed by a size. For example, the instance type c5n.xlarge can be broken down as follows:

- **First position –** The first position, **c**, indicates the instance family. This indicates that this instance belongs to the compute optimized family.
- **Second position –** The second position, **5**, indicates the generation of the instance. This instance belongs to the fifth generation of instances.
- **Remaining letters before the period –** In this case, **n** indicates additional attributes, such as local NVMe storage.
- **After the period –** After the period, **xlarge** indicates the instance size. In this example, it's xlarge.
 
![[Pasted image 20240729115337.jpg]]

| **Instance family**             | **Description**                                                                                                                                                                                                                                                                                                            | **Use Cases**                                                                                                                                                                                                                                                            |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **General purpose  <br>**       | General purpose instances provide a balance of compute, memory, and networking resources, and can be used for a variety of workloads.                                                                                                                                                                                      | Ideal for applications that use these resources in equal proportions, such as web servers and code repositories                                                                                                                                                          |
| **Compute optimized  <br>**     | Compute optimized instances are ideal for compute-bound applications that benefit from high-performance processors.                                                                                                                                                                                                        | Well-suited for batch processing workloads, media transcoding, high performance web servers, high performance computing (HPC), scientific modeling, dedicated gaming servers and ad server engines, machine learning inference, and other compute intensive applications |
| **Memory optimized  <br>**      | Memory optimized instances are designed to deliver fast performance for workloads that process large datasets in memory.                                                                                                                                                                                                   | Memory-intensive applications, such as high-performance databases, distributed web-scale in-memory caches, mid-size in-memory databases, real-time big-data analytics, and other enterprise applications                                                                 |
| **Accelerated computing  <br>** | Accelerated computing instances use hardware accelerators or co-processors to perform functions such as floating-point number calculations, graphics processing, or data pattern matching more efficiently than is possible in software running on CPUs.                                                                   | Machine learning, HPC, computational fluid dynamics, computational finance, seismic analysis, speech recognition, autonomous vehicles, and drug discovery                                                                                                                |
| **Storage optimized  <br>**     | Storage optimized instances are designed for workloads that require high sequential read and write access to large datasets on local storage. They are optimized to deliver tens of thousands of low-latency random I/O operations per second (IOPS) to applications that replicate their data across different instances. | NoSQL databases (Cassandra, MongoDB and Redis), in-memory databases, scale-out transactional databases, data warehousing, Elasticsearch, and analytics                                                                                                                   |
| **HPC optimized  <br>**         | High performance computing (HPC) instances are purpose built to offer the best price performance for running HPC workloads at scale on AWS.                                                                                                                                                                                | Ideal for applications that benefit from high-performance processors, such as large, complex simulations and deep learning workloads                                                                                                                                     |## 

## EC2 instance locations

[Default VPCs](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html)

Unless otherwise specified, when you launch EC2 instances, they are placed in a default virtual private cloud (VPC). Any resource that you put inside the default VPC will be public and accessible by the internet, so you shouldn’t place any customer data or private information in it.
### Architecting for high availability

[Reliability Pillar - AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html?ref=wellarchitected-wp)

AWS services that are scoped at the Availability Zone level must be architected with high availability in mind.

Although EC2 instances are typically reliable, two are better than one, and three are better than two. Specifying the instance size gives you an advantage when designing your architecture because you can use more smaller instances rather than a few larger ones.

When architecting any application for high availability, consider using at least two EC2 instances in two separate Availability Zones. ­­