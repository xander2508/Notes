The distinction of responsibility is commonly referred to as security **_of_** the cloud as compared to security _**in**_ the cloud.

![[Pasted image 20240726153834.png]]

## AWS responsibility

AWS is responsible for security of the cloud. This means that AWS protects and secures the infrastructure that runs the services offered in the AWS Cloud. AWS is responsible for the following:

- Protecting and securing AWS Regions, Availability Zones, and data centers, down to the physical security of the buildings
- Managing the hardware, software, and networking components that run AWS services, such as the physical servers, host operating systems, virtualization layers, and AWS networking components

The level of responsibility that AWS has depends on the service. AWS classifies services into two categories.

| **Category**                      | **Examples of AWS Services in the Category**                                                                      | **AWS Responsibility**                                                                                                             |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Infrastructure services  <br>** | Compute services, such as Amazon Elastic Compute Cloud (Amazon EC2)                                               | AWS manages the underlying infrastructure and foundation services.                                                                 |
| **Abstracted services  <br>**     | Services that require very little management from the customer, such as Amazon Simple Storage Service (Amazon S3) | AWS operates the infrastructure layer, operating system, and platforms, in addition to server-side encryption and data protection. |

## Customer responsibility

Customers are responsible for security in the cloud. When using any AWS service, the customer is responsible for properly configuring the service and their applications, in addition to ensuring that their data is secure.