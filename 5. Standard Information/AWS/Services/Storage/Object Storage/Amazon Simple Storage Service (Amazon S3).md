
[Amazon S3](https://aws.amazon.com/s3/)

Amazon Simple Storage Service (Amazon S3) is a standalone storage solution that isn’t tied to compute. With Amazon S3, you can retrieve your data from anywhere on the web.

Amazon S3 is an object storage service. Object storage stores data in a flat structure. An object is a file combined with metadata. You can store as many of these objects as you want. All the characteristics of object storage are also characteristics of Amazon S3.

In Amazon S3, you store your objects in containers called buckets. When you store an object in a bucket, the combination of a bucket name, key, and version ID uniquely identifies the object.

 S3 store data in a minimum of three Availability Zones
### Amazon S3 bucket names

[Bucket Naming Rules](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html)

Amazon S3 supports global buckets. Therefore, each bucket name must be unique across all AWS accounts in all AWS Regions within a partition. A partition is a grouping of Regions, of which AWS currently has three: Standard Regions, China Regions, and AWS GovCloud (US). 

When naming a bucket, choose a name that is relevant to you or your business. For example, you should avoid using AWS or Amazon in your bucket name.

The following are some examples of the rules that apply for naming buckets in Amazon S3. For a full list of rules, see the link in the resources section. 

- Bucket names must be between 3 (min) and 63 (max) characters long.
- Bucket names can consist only of lowercase letters, numbers, dots (.), and hyphens (-).
- Bucket names must begin and end with a letter or number.
- Buckets must not be formatted as an IP address.
- A bucket name cannot be used by another AWS account in the same partition until the bucket is deleted.

If your application automatically creates buckets, choose a bucket naming scheme that is unlikely to cause naming conflicts and will choose a different bucket name, should one not be available.


## Object key names

The object key (key name) uniquely identifies the object in an Amazon S3 bucket. When you create an object, you specify the key name. 

As described earlier, the Amazon S3 model is a flat structure, meaning there is no hierarchy of sub buckets or subfolders. However, the Amazon S3 console does support the concept of folders. By using key name prefixes and delimiters, you can imply a logical hierarchy.

For example, suppose your bucket called _testbucket_ has two objects with the following object keys: _2022-03-01/AmazonS3.html_ and _2022-03-01/Cats.jpg_. The console uses the key name prefix, _2022-03-01_, and delimiter (_/_) to present a folder structure.

![[Pasted image 20240730100642.png]]


## Amazon S3 use cases

Amazon S3 is a widely used storage service, with far more use cases than could fit on one screen. To learn more, expand each of the following six categories.

- Backup and storage
- Media hosting
- Software delivery
- Data lakes
- Static websites
- Static content

## Security in Amazon S3

Everything in Amazon S3 is private by default. This means that all Amazon S3 resources, such as buckets and objects, can only be viewed by the user or AWS account that created that resource. Amazon S3 resources are all private and protected to begin with.

A public resource means that everyone on the internet can see it.

To be more specific about who can do what with your Amazon S3 resources, Amazon S3 provides several security management features: [[IAM Policies]], S3 bucket policies, and encryption to develop and implement your own security policies.

### IAM Policies 

[Bucket Policy Examples](https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/example-bucket-policies.html)

Access policies that you attach to your resources are referred to as _resource-based policies_ and access policies attached to users in your account are called *user policies*

You should use IAM policies for private buckets in the following two scenarios:

- You have many buckets with different permission requirements. Instead of defining many different S3 bucket policies, you can use IAM policies.
- You want all policies to be in a centralized location. By using IAM policies, you can manage all policy information in one location.

### S3 Bucket Policies
 
 S3 bucket policies can only be attached to S3 buckets. The policy that is placed on the bucket applies to every object in that bucket. S3 bucket policies specify what actions are allowed or denied on the bucket.
 
 You should use S3 bucket policies in the following scenarios:

- You need a simple way to do cross-account access to Amazon S3, without using IAM roles.
- Your IAM policies bump up against the defined size limit. S3 bucket policies have a larger size limit.

See [Bucket Policy Examples](https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/example-bucket-policies.html).


## Amazon S3 encryption

Amazon S3 reinforces encryption in transit (as it travels to and from Amazon S3) and at rest. To protect data, Amazon S3 automatically encrypts all objects on upload and applies server-side encryption with S3-managed keys as the base level of encryption for every bucket in Amazon S3 at no additional cost.


## Amazon S3 Storage Classes

[Amazon S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/)

Amazon S3 storage classes let you change your storage tier when your data characteristics change. For example, if you are accessing your old photos infrequently, you might want to change the storage class for the photos to save costs.

| **Storage Class**                                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **S3 Standard**                                    | This is considered general-purpose storage for cloud applications, dynamic websites, content distribution, mobile and gaming applications, and big data analytics.                                                                                                                                                                                                                                                                                                                                                                    |
| **S3 Intelligent-Tiering**                         | This tier is useful if your data has unknown or changing access patters. S3 Intelligent-Tiering stores objects in three tiers: a frequent access tier, an infrequent access tier, and an archive instance access tier. Amazon S3 monitors access patterns of your data and automatically moves your data to the most cost-effective storage tier based on frequency of access.                                                                                                                                                        |
| **S3 Standard-Infrequent Access (S3 Standard-IA)** | This tier is for data that is accessed less frequently but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, and low latency of S3 Standard, with a low per-GB storage price and per-GB retrieval fee. This storage tier is ideal if you want to store long-term backups, disaster recovery files, and so on.                                                                                                                                                                            |
| **S3 One Zone-Infrequent Access (S3 One Zone-IA)** | Unlike other S3 storage classes that store data in a minimum of three Availability Zones, S3 One Zone-IA stores data in a single Availability Zone, which makes it less expensive than S3 Standard-IA. S3 One Zone-IA is ideal for customers who want a lower-cost option for infrequently accessed data, but do not require the availability and resilience of S3 Standard or S3 Standard-IA. It's a good choice for storing secondary backup copies of on-premises data or easily recreatable data.                                 |
| **S3 Glacier Instant Retrieval**                   | Use S3 Glacier Instant Retrieval for archiving data that is rarely accessed and requires millisecond retrieval. Data stored in this storage class offers a cost savings of up to 68 percent compared to the S3 Standard-IA storage class, with the same latency and throughput performance.                                                                                                                                                                                                                                           |
| **S3 Glacier Flexible Retrieval**                  | S3 Glacier Flexible Retrieval offers low-cost storage for archived data that is accessed 1–2 times per year. With S3 Glacier Flexible Retrieval, your data can be accessed in as little as 1–5 minutes using an expedited retrieval. You can also request free bulk retrievals in up to 5–12 hours. It is an ideal solution for backup, disaster recovery, offsite data storage needs, and for when some data occasionally must be retrieved in minutes.                                                                              |
| **S3 Glacier Deep Archive**                        | S3 Glacier Deep Archive is the lowest-cost Amazon S3 storage class. It supports long-term retention and digital preservation for data that might be accessed once or twice a year. Data stored in the S3 Glacier Deep Archive storage class has a default retrieval time of 12 hours. It is designed for customers that retain data sets for 7–10 years or longer, to meet regulatory compliance requirements. Examples include those in highly regulated industries, such as the financial services, healthcare, and public sectors. |
| **S3 on Outposts**                                 | Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment using S3 API's and features. For workloads that require satisfying local data residency requirements or need to keep data close to on premises applications for performance reasons, the S3 Outposts storage class is the ideal option.                                                                                                                                                                                                    |


## Amazon S3 Versioning

Without Amazon S3 versioning, every time you upload an object called employee.jpg to the employees bucket, it will overwrite the original object.  
This can be an issue for several reasons, including the following:

- **Common names:** The employee.jpg object name is a common name for an employee photo object. You or someone else who has access to the bucket might not have intended to overwrite it; but once it's overwritten, the original object can't be accessed.
- **Version preservation:** You might want to preserve different versions of employee.jpg. Without versioning, if you wanted to create a new version of employee.jpg, you would need to upload the object and choose a different name for it. Having several objects all with slight differences in naming variations can cause confusion and clutter in S3 buckets.

Versioning keeps multiple versions of a single object in the same bucket. This preserves old versions of an object without using different names, which helps with object recovery from accidental deletions, accidental overwrites, or application failures.

If you enable versioning for a bucket, Amazon S3 automatically generates a unique version ID for the object.

By using versioning-enabled buckets, you can recover objects from accidental deletion or overwrite. The following are examples:

- Deleting an object does not remove the object permanently. Instead, Amazon S3 puts a marker on the object that shows that you tried to delete it. If you want to restore the object, you can remove the marker and the object is reinstated.
- If you overwrite an object, it results in a new object version in the bucket. You still have access to previous versions of the object.

### Versioning states

[Using Versioning in S3 Buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)

Buckets can be in one of three states. The versioning state applies to all objects in the bucket. Storage costs are incurred for all objects in your bucket, including all versions. To reduce your Amazon S3 bill, you might want to delete previous versions of your objects when they are no longer needed.

#### Unversioned (default)

No new and existing objects in the bucket have a version.

#### Versioning-enabled

Versioning is enabled for all objects in the bucket. After you version-enable a bucket, it can never return to an unversioned state. However, you can suspend versioning on that bucket.

#### Versioning-suspended

Versioning is suspended for new objects. All new objects in the bucket will not have a version. However, all existing objects keep their object versions.


## Managing your Storage Lifecycle

When you define a lifecycle configuration for an object or group of objects, you can choose to automate between two types of actions: transition and expiration.

- **Transition actions** define when objects should transition to another storage class.
- **Expiration actions** define when objects expire and should be permanently deleted.

For example, you might transition objects to S3 Standard-IA storage class 30 days after you create them. Or you might archive objects to the S3 Glacier Deep Archive storage class 1 year after creating them.