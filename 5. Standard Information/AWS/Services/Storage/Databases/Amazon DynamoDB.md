DynamoDB is a fully managed NoSQL database that provides fast, consistent performance at any scale. 

It has a flexible billing model, tight integration with infrastructure as code (IaC), and a hands-off operational model. 

DynamoDB has become the database of choice for two categories of applications: high-scale applications and serverless applications. 

Although DynamoDB is the database of choice for high-scale and serverless applications, it can work for nearly all online transaction processing (OLTP) application workloads. 

With DynamoDB, you can do the following:

- Create database tables that can store and retrieve any amount of data and serve any level of request traffic. 
- Scale up or scale down your tables' throughput capacity without downtime or performance degradation. 
- Monitor resource usage and performance metrics using the AWS Management Console.

DynamoDB automatically spreads the data and traffic for your tables over a sufficient number of servers to handle your throughput and storage requirements. It does this while maintaining consistent, fast performance. All your data is stored on SSDs and is automatically replicated across multiple Availability Zones in a Region, providing built-in high availability and data durability.


## DynamoDB core components

In DynamoDB, tables, items, and attributes are the core components that you work with. A table is a collection of items, and each item is a collection of attributes. DynamoDB uses primary keys to uniquely identify each item in a table and secondary indexes to provide more querying flexibility.

![[Pasted image 20240730133633.png]]

## DynamoDB use cases


- You are experiencing scalability problems with other traditional database systems.
- You are actively engaged in developing an application or service.
- You are working with an OLTP workload.
- You care deploying a mission-critical application that must be highly available at all times without manual intervention.
- You require a high level of data durability, regardless of your backup-and-restore strategy.