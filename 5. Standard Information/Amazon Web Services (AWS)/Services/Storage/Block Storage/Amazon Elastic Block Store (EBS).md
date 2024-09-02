---
tags:
  - AWS
  - AmazonWebServices
  - Services
  - Storage
  - BlockStorage
---

[Amazon Elastic Block Store (Amazon EBS)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
[Amazon EBS](https://aws.amazon.com/ebs/faqs/)

As the name implies, Amazon Elastic Block Store (Amazon EBS) is block-level storage that you can attach to an Amazon EC2 instance. You can compare this to how you much attach an external drive to your laptop. This attachable storage is called an EBS volume. 

EBS volumes act similarly to external drives in more than one way.

- **Detachable:** You can detach an EBS volume from one EC2 instance and attach it to another EC2 instance in the same Availability Zone to access the data on it.
- Distinct:** The external drive is separate from the computer. That means that if an accident occurs and the computer goes down, you still have your data on your external drive. The same is true for EBS volumes.
- Size-limited:** You’re limited to the size of the external drive, because it has a fixed limit to how scalable it can be. For example, you might have a 2 TB external drive, which means you can only have 2 TB of content on it. This also relates to Amazon EBS, because a volume also has a max limitation of how much content you can store on it.
- **1-to-1 connection:** Most EBS volumes can only be connected with one computer at a time. Most EBS volumes have a one-to-one relationship with EC2 instances, so they cannot be shared by or attached to multiple instances at one time.

## Scaling Amazon EBS volumes

### Increase Volume Size

**Increase the volume size** only if it doesn’t increase above the maximum size limit. Depending on the volume selected, Amazon EBS currently supports a maximum volume size of 64 tebibytes (TiB).

For example, if you provision a 5-TiB io2 Block Express volume, you can choose to increase the size of your volume until you get to 64 TiB.

## Attach Multiple Volumes

**Attach multiple volumes** to a single EC2 instance. Amazon EC2 has a one-to-many relationship with EBS volumes. You can add these additional volumes during or after EC2 instance creation to provide more storage capacity for your hosts.

## Amazon EBS use cases

Amazon EBS is useful when you must retrieve data quickly and have data persist long term. Volumes are commonly used in the following scenarios.

#### Operating systems

Boot and root volumes can be used to store an operating system. The root device for an instance launched from an Amazon Machine Image (AMI) is typically an EBS volume. These are commonly referred to as EBS-backed AMIs.

#### Databases

As a storage layer for databases running on Amazon EC2 that will scale with your performance needs and provide consistent and low-latency performance.

#### Enterprise applications

Amazon EBS provides high availability and high durability block storage to run business-critical applications.

#### Big data analytics engines

Amazon EBS offers data persistence, dynamic performance adjustments, and the ability to detach and reattach volumes, so you can resize clusters for big data analytics.


## EBS volume types

EBS volumes are organized into two main categories: solid-state drives (SSDs) and hard-disk drives (HDDs). 

SSDs are used for transactional workloads with frequent read/write operations with small I/O size. 

HDDs are used for large streaming workloads that need high throughput performance.  

AWS offers two types of each.

|                                   | **General Purpose**   <br>**SSD volumes**                                                 |           | **Provisioned IOPS**   <br>**SSD volumes**                                           |             |     |
| --------------------------------- | ----------------------------------------------------------------------------------------- | --------- | ------------------------------------------------------------------------------------ | ----------- | --- |
| **Volume type**                   | gp3                                                                                       | gp2       | io2 Block Express                                                                    | io2         | io1 |
| **Description**                   | Provides a balance of price and performance for a wide variety of transactional workloads |           | Provides high-performance SSD designed for latency-sensitive transactional workloads |             |     |
| **Volume size**                   | 1 GiB–16 TiB                                                                              |           | 4 GiB–64 TiB                                                                         | 4GiB–16 TiB |     |
| **Max IOPS**   <br>**per volume** | 16,000                                                                                    |           | 256,000                                                                              | 64,000      |     |
| **Max throughput per volume**     | 1,000 MiB/s                                                                               | 250 MiB/s | 4,000 MiB/s                                                                          | 1,000 MiB/s |     |
| **Amazon EBS Multi-attach**       | Not supported                                                                             |           | Supported                                                                            |             |     |


|                               | **Throughput Optimized HDD volumes**                                            | **Cold HDD volumes**                                                |
| ----------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Volume type**               | st1                                                                             | sc1                                                                 |
| **Description**               | A low-cost HDD designed for frequently accessed, throughput-intensive workloads | The lowest cost HDD designed for less frequently accessed workloads |
| **Volume size**               | 125 GiB–16 TiB                                                                  |                                                                     |
| **Max IOPS per volume**       | 500                                                                             | 250                                                                 |
| **Max throughput per volume** | 500 MiB/s                                                                       | 250 MiB/s                                                           |
| **Amazon EBS Multi-attach**   | Not supported                                                                   |                                                                     |

## Amazon EBS benefits

- When you create an EBS volume, it is automatically replicated in its Availability Zone to prevent data loss from single points of failure.
- Storage persists even when your instance doesn’t.
- When activated by the user, all EBS volumes support encryption. 
- EBS volumes support on-the-fly changes. Modify volume type, volume size, and input/output operations per second (IOPS) capacity without stopping your instance.
- Amazon EBS provides the ability to create backups of any EBS volume.


## Amazon EBS snapshots

EBS snapshots are incremental backups that only save the blocks on the volume that have changed after your most recent snapshot. For example, if you have 10 GB of data on a volume and only 2 GB of data have been modified since your last snapshot, only the 2 GB that have been changed are written to Amazon S3.

When you take a snapshot of any of your EBS volumes, the backups are stored redundantly in multiple Availability Zones using Amazon S3. This aspect of storing the backup in Amazon S3 is handled by AWS, so you won’t need to interact with Amazon S3 to work with your EBS snapshots. You manage them in the Amazon EBS console, which is part of the Amazon EC2 console.  
  
EBS snapshots can be used to create multiple new volumes, whether they’re in the same Availability Zone or a different one. When you create a new volume from a snapshot, it’s an exact copy of the original volume at the time the snapshot was taken.