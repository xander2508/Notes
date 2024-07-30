Amazon RDS is a managed database service customers can use to create and manage relational databases in the cloud without the operational burden of traditional database management.

Amazon RDS supports most of the popular RDBMSs, ranging from commercial options to open-source options and even a specific AWS option. Supported Amazon RDS engines include the following:

- **Commercial:** Oracle, SQL Server
- **Open source:** MySQL, PostgreSQL, MariaDB
- **Cloud native:** Aurora

## Database Instances

Just like the databases you build and manage yourself, Amazon RDS is built from compute and storage. The compute portion is called the database (DB) instance, which runs the DB engine.

A DB instance can contain multiple databases with the same engine, and each DB can contain multiple tables.

Underneath the DB instance is an [[Amazon Elastic Compute Cloud (EC2)]] instance. However, this instance is managed through the Amazon RDS console instead of the Amazon EC2 console. The DB instance class you choose affects how much processing power and memory it has.

## Storage on Amazon RDS

The storage portion of DB instances for Amazon RDS use [[Amazon Elastic Block Store (EBS)]] volumes for database and log storage. This includes MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server.

When using Aurora, data is stored in cluster volumes, which are single, virtual volumes that use solid-state drives (SSDs). A cluster volume contains copies of your data across three Availability Zones in a single AWS Region. For nonpersistent, temporary files, Aurora uses local storage.

Amazon RDS provides three storage types: General Purpose SSD (also called gp2 and gp3), Provisioned IOPS SSD (also called io1), and Magnetic (also called standard). They differ in performance characteristics and price, which means you can tailor your storage performance and cost to the needs of your database workload. See [[Amazon Elastic Block Store (EBS)#EBS volume types]]

## Amazon RDS in an Amazon Virtual Private Cloud

When you create a DB instance, you select the Amazon Virtual Private Cloud (Amazon VPC) your databases will live in. Then, you select the subnets that will be designated for your DB. This is called a DB subnet group, and it has at least two Availability Zones in its Region. The subnets in a DB subnet group should be private, so they don’t have a route to the internet gateway. This ensures that your DB instance, and the data inside it, can be reached only by the application backend.

## Backup data

You don’t want to lose your data. To take regular backups of your Amazon RDS instance, you can use automated backups or manual snapshots. To learn about a category, choose the appropriate tab.

### Automated Backups

Automated backups are turned on by default.

This backs up your entire DB instance (not just individual databases on the instance) and your transaction logs. 

When you create your DB instance, you set a backup window that is the period of time that automatic backups occur. Typically, you want to set the window during a time when your database experiences little activity because it can cause increased latency and downtime.

Automated backups are retained between 0 and 35 days.

> [!NOTE]
> The 0 days setting stops automated backups from happening. If you set it to 0, it will also delete all existing automated backups. This is not ideal.


**Point-in-time recovery:** This creates a new DB instance using data restored from a specific point in time. This restoration method provides more granularity by restoring the full backup and rolling back transactions up to the specified time range.

### Manual Snapshots

If you want to keep your automated backups longer than 35 days, use manual snapshots.

Manual snapshots are similar to taking Amazon EBS snapshots, except you manage them in the Amazon RDS console. These are backups that you can initiate at any time. They exist until you delete them.

If you restore data from a manual snapshot, it creates a new DB instance using the data from the snapshot.


## Redundancy with Amazon RDS Multi-AZ