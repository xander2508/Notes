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

Unless otherwise specified, when you launch EC2 instances, they are placed in a default [[Amazon Virtual Private Cloud (VPC)]]. Any resource that you put inside the default VPC will be public and accessible by the internet, so you shouldn’t place any customer data or private information in it.
### Architecting for high availability

[Reliability Pillar - AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html?ref=wellarchitected-wp)

AWS services that are scoped at the Availability Zone level must be architected with high availability in mind.

Although EC2 instances are typically reliable, two are better than one, and three are better than two. Specifying the instance size gives you an advantage when designing your architecture because you can use more smaller instances rather than a few larger ones.

When architecting any application for high availability, consider using at least two EC2 instances in two separate Availability Zones. ­­

# Instance Lifecycle

[Amazon EC2: Instance Lifecycle](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)
[Hibernation Prerequisites](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hibernating-prerequisites.html)

An EC2 instance transitions between different states from the moment you create it until its termination.

![[Pasted image 20240729133859.png]]

When you stop an instance, it enters the stopping state until it reaches the stopped state. AWS does not charge usage or data transfer fees for your instance after you stop it. But storage for any Amazon EBS volumes is still charged. While your instance is in the stopped state, you can modify some attributes, like the instance type. When you stop your instance, the data from the instance memory (RAM) is lost.  
  
When you stop-hibernate an instance, Amazon EC2 signals the operating system to perform hibernation (suspend-to-disk), which saves the contents from the instance memory (RAM) to the EBS root volume. You can hibernate an instance only if hibernation is turned on and the instance meets the hibernation prerequisites.


# Pricing

[Amazon EC2 Pricing](https://aws.amazon.com/ec2/pricing/)
[Amazon EC2 On-Demand Pricing(opens in a new tab)](https://aws.amazon.com/ec2/pricing/on-demand/)
[Amazon EC2 Spot Instances Pricing(opens in a new tab)](https://aws.amazon.com/ec2/spot/pricing/)
[Amazon EC2 Reserved Instances Pricing](https://aws.amazon.com/ec2/pricing/reserved-instances/pricing/)

| Type                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| On-Demand Instances | Pay for compute capacity per hour or per second, depending on which instances that you run. There are no long-term commitments or upfront payments required. Billing begins whenever the instance is running, and billing stops when the instance is in a stopped or terminated state. <br><br>- Users who prefer the low cost and flexibility of Amazon EC2 without upfront payment or long-term commitments                <br><br>- Applications with short-term, spiky, or unpredictable workloads that cannot be interrupted<br><br>- Applications being developed or tested on Amazon EC2 for the first time                                                                                                                                                                                                                                                                                                                                                                          |
| Spot Instances      | For applications that have flexible start and end times.<br>Amazon EC2 Spot Instances, you can request spare Amazon EC2 computing capacity for up to 90 percent off the On-Demand price.<br><br>- Applications that have flexible start and end times            <br>    <br>- Applications that are only feasible at very low compute prices            <br>    <br>- Users with fault-tolerant or stateless workloads<br><br>With Spot Instances, you set a limit on how much you want to pay for the instance hour. This is compared against the current Spot price that AWS determines. Spot Instance prices adjust gradually based on long-term trends in supply and demand for Spot Instance capacity.                                                                                                                                                                                                                                                                                |
| Savings Plans       | Flexible pricing model that offers low usage prices for a 1-year or 3-year term commitment to a consistent amount of usage.<br><br>Savings Plans apply to Amazon EC2, [[AWS Lambda]], and [[AWS Fargate]] usage and provide up to 72 percent savings on AWS compute usage.<br><br>- Workloads with a consistent and steady-state usage            <br>    <br>- Customers who want to use different instance types and compute solutions across different locations        <br>    <br>- Customers who can make monetary commitment to use Amazon EC2 over a 1-year or 3-year term<br>                                                                                                                                                                                                                                                                                                                                                                                                      |
| Reserved Instances  | Save up to 75 percent compared to On-Demand Instance pricing. You can choose between three payment options: All Upfront, Partial Upfront, or No Upfront.<br><br>With Reserved Instances, you can choose the type that best fits your applications needs.     <br><br>- Standard Reserved Instances: These provide the most significant discount (up to 72 percent off On-Demand pricing) and are best suited for steady-state usage.     <br><br>- Convertible Reserved Instances: These provide a discount (up to 54 percent off On-Demand pricing) and the capability to change the attributes of the Reserved Instance if the exchange results in the creation of Reserved Instances of equal or greater value.<br><br>- Scheduled Reserved Instances: These are available to launch within the time windows that you reserve. With this option, you can match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, a week, or a month. |
| Dedicated Host      | A physical Amazon EC2 server that is dedicated for your use.<br><br>Dedicated Hosts can help you reduce costs because you can use your existing server-bound software licenses, such as Windows Server, SQL Server, and Oracle licenses. And they can also help you meet compliance requirements. Amazon EC2 Dedicated Host is also integrated with [[AWS License Manager]], a service that helps you manage your software licenses, including Microsoft Windows Server and Microsoft SQL Server licenses.<br><br>- Dedicated Hosts can be purchased on demand (hourly).<br><br>- Dedicated Hosts can be purchased as a Reservation for up to 70 percent off the On-Demand price.                                                                                                                                                                                                                                                                                                           |
