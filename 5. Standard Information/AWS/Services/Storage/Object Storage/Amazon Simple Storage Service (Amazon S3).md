Amazon Simple Storage Service (Amazon S3) is a standalone storage solution that isn’t tied to compute. With Amazon S3, you can retrieve your data from anywhere on the web.

Amazon S3 is an object storage service. Object storage stores data in a flat structure. An object is a file combined with metadata. You can store as many of these objects as you want. All the characteristics of object storage are also characteristics of Amazon S3.

In Amazon S3, you store your objects in containers called buckets. When you store an object in a bucket, the combination of a bucket name, key, and version ID uniquely identifies the object.

### Amazon S3 bucket names

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