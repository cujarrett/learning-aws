# Databases

## Relational Database vs Non Relational Database
### Relational Database
A Relational Database are what most of us are all used to. They have been around since the 70's. Think of a traditional spreadsheet.
- Databases
- Tables
- Row
- Fields

### Non Relational Database
- Collection = Table
- Document = Row
- Key Value Pair = Fields

## RDS (Relational Database Service)
- Used in Online Transactional Processing (OLTP)

AWS RDS Offerings
  - SQL Server
  - Oracle
  - MySQL Server
  - PostgreSQL
  - Aurora
  - MariaDB

### RDS Key Features
- Multi Availability Zone - For disaster recovery
- Read Replicas - For performance
  - You can have up to 5 copies of Read Replica in RDS
- RDS runs on virtual machines
  - You cannot log into (ssh) these operating systems however
- Patching of the RDS Operating System and DB is Amazon's responsibility
- RDS is not Serverless (with the exception of Aurora Serverless)

### Backups With RDS
- **Automated Backups** - Allow you to recover your database to any point in time within a retention period. The retention period can be between 1 and 35 days. Automated Backups will take a full daily snapshot and will also store transactional logs throughout the day. When you do a recovery, AWS will first choose the most recent daily backup, and then apply transactional logs relevent to that day. This allows you to do point in time recovery down to a second, within the retention period.

  Automated Backups are enabled by default. The backup data is stored in S3 and you get free storage equal to the size of your database. So if you have an RDS instance of 10Gb, you will get 10Gb worth of storage.

  Backups are taken within a defined maintenance window. During the backup window, storage I/O may be suspended while your data is being backed up and you may expereince elevated latency.
  
- **Database Snapshots** - Done manually, (ie they are user intiated). They are stored even after you delete the orginal RDS instance, unlike automated backups.

### Restoring Backups With RDS
Whenever you restore either an Automated Backup or Snapshot Backup, the restored verson of the database will be a new RDS instance with a new DNS endpoint.

![backups-get-a-new-dns-endpoint](https://user-images.githubusercontent.com/16245634/70203166-a599e380-16e1-11ea-9f88-52a76e175825.png)

_image from [A Cloud Guru](https://acloud.guru/)_

### RDS Encryption At Rest
Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB, Aurora. Encryption is done using the AWS Key Management Service (KMS). Once your RDS instance is encrypted, as are its backups, read replicas, and snapshots.

Encryption at rest is available for the following RDS database types:
- MySQL
- Oracle
- SQL Server
- PostgreSQL
- MariaDB
- Aurora

### RDS Multi-AZ (Multiple Availability Zone)
Multi-AZ allows you to have an exact copy of your production database in another Availability Zone. AWS handles the replicatoon for you, so when your production database is written to, this write will automatically be synchronized to the stand by database.

In the event of planned database maintenance, DB instance failure, or an Availability Zone failure, Amazon RDS will automatically failover to the standby so that database operations can resume quickly without administrative intervention.

Multi-AZ is for Disaster Recovery only. It is not primarily used for improving performance. For performance improvement, you need Read Replicas.

You can force a failover from one Availability Zone to another by rebooting the RDS instance.

Multi-AZ is available for the following RDS database types:
- SQL Server
- Oracle
- MySQL Server
- PostgreSQL
- MariaDB

(Aurora is completely fault tollerent by design)

### RDS Read Replica
Read Replicas allow you to have a read-only copy of your production database. This is achieved by using Asynchronous replication from the primary RDS instance to the read replica. You use read replicas primarily for very read-havy database workloads.

- Used for scaling, not Disaster Recovery. Used to increase performance.
- Must have automatic backups turned on in order to deploy a read replica
- You can have up to 5 read replica copies of any database
- You can have read replicas of read replicas (but watch out for latency)
- Each read replica will have its own DNS endpoint
- You can have read replicas that have Multi-AZ
- You can create read replicas of Multi-AZ source databases
- Read replicas can be promoted to be their own databases. This breaks the replication.
- You can have a read replica in a second region

Read Replicas are available for the following RDS database types:
- MySQL Server
- PostgreSQL
- MariaDB
- Oracle
- Aurora

## Aurora
Amazon Aurora is a MySQL-compatible, relational database engine that combines the speed and availability of high end commercial databases with the simplicity and cost effectiveness of open source databases. Amazon Aurora provides up to five times better performance than MySQL at a price point one tenth that of a commercial database while delivering similar performance and availability.

- 2 copies of your data is contained in each Availability Zone, with a minimum of 3 Availability Zones. 6 copies of your data.
- Starts with 10GB, scales in 10GB increments to 64TB (Storage Autoscaling)
- Compute resources can scale up to 32vCPUs and 244GB of Memory

### Aurora Scaling
- Aurora is designed to transparently handle the loss of up to two copies of data without affecting database write availability and up to three copies without affecting read availability.
- Aurora storage is self healing. Data blocks and disks are continuously scanned for errors adn repaired automatically.

### Aurora Read Replicas
- Aurora Replicas (currently 15) - Automated failover is only available with Aurora Replicas
- MySQL Read Replicas (currently 5)

### Aurora Backups
- Automated backups are always enabled on Amazon Aurora DB instances. Backups do not impact database performance.
- You can also take snapshots with Aurora. This also does not impact performance.
- You can share Aurora Snapshots with oter AWS accounts

## Data Warehousing
Used for business intelligence. Tools like Congos, Jaspersoft, SQL Server Reporting Services, Oracle Hyperion, SAP NetWeaver.

- Used to pull in very large and complex data sets. Usually used by management to do queries on data (such as current performance vs targets etc)
- Data Warehousing databases use different types of architecture both from a database perspective and infrastructure layer.
- Amazon's Data Warehouse solution is called Redshift

AWS Data Warehousing Offerings
  - Red Shift - For Online Analytics Processing (OLAP)

### Online Transactional Processing (OLTP) vs Online Analytics Processing (OLAP)
Online Transactional Processing (OLTP) differes from Online Analytics Processing (OLAP) in terms of the types of queries you will run.

OLTP Example:
```
Order number 2120121
Pulls up a row of data such as
Name, Date, Address to Deliver to, Delivery Status, etc
```

OLAP Example:
```
Net profit for EMEA and Pacific for the Digital Radio Product.
Pulls in large numbers of records

Sum of Radios Sold in EMEA
Sum of Radios Sold in Pacific
Unit Cost of Radio in each region
Sales price of each radio
Sales price - Unit cost.
```

## Redshift
Redshift is Amazons Data Warehousing soltuion. Redshift is a fast and powerful, fully managed, petabyte-scale service in the cloud. Customers can start small for just $.025 per hour with no commitments or upfront costs and scale to a petabyte or more for $1,000 per terabyte per year, less than a tenth of most other data warehousing solutions.

- Redshift is used for Business Intelligence
- Available in only 1 Availability Zone

### Redshift Configuration Options
- Single Node (160Gb)
- Multi-Node is made up of:
  - Leader Node - Manages client connections and recieves queries
  - Compute Node - Store data and perform queries and computations. Up to 128 Compute Nodes.

### Redshift Compression
Redshift uses advanced compresion. Columnar data stores can be compressed much more than row-based data stores becuase similar data is stored sequentually on disk. Amazon Redshift employs multiple compression techniques and can often achieve significant compression relative to traditional relational data stores. In addition, Amazon Redshift doesn't require indexes or materialized views, and so uses less space than traditional relational database systems. When loading data into an empty table, Amazon Redshift automatically samples your data and selects the most appropiate compression scheme.

### Redshift Backups
- Enabled by default with a 1 day retention period
- Maxium retention period is 35 days
- Redshift always attempts to maintain at least three copies of your data (the orginal and replica on the compute nodes and a backup in S3)
- Redshift can also asynchronously replicate your snapshots to S3 in another region for disaster recovery

### Redshift Parallel Processing
Redshift uses Massively Parallel Processing (MPP) automically to distribute data and query load across all nodes. Amazon Redshift makes it easy to add nodes to your data warehouse and enables you to maintian fast query performance as your data warehouse grows.

### Redshift Pricing
- Compute Node Hours (total number of hours you run across all your compute nodes for the billing period. You are billed for 1 unit per node per hour. For example, a 3 node data warehouse cluster running persistently for an entire month would incure 2,160 instance hours. You will not be charged for the leader node hours, only compute nodes will incur charges.
- Backup(s)
- Data Transfer (only within a VPC, not outside it)

### Redshift Security Considerations
- Encrypted in transit using SSL
- Encrypted at rest using AES-256 encryption
- By default Redshift takes care of key management
  - You could manage your own keys through HSM
  - AWS Key Management Service

### Redshift Availability
- Currently only available in 1 Availability Zone
- Can restore snapshots to new Availability Zones in the event of an outage

## ElastiCache
ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

- Use ElastiCache to uncrease databases (frequent identical queries) and web application performance

AWS ElastiCache supports two open-source in-memory caching engines
  - Memcached
  - Redis

### Memcached vs Redis
![memcached vs redis chart](https://user-images.githubusercontent.com/16245634/70358428-efe4a700-183e-11ea-99dd-6de1c37b271a.png)

- Redis is Multi Avability Zone
- You can do backups and restores of Redis
  
## DynamoDB
Fast and flexiable NOSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

- Stored on SSD storage
- Spread across 3 geographically distinct data centres
- Eventual Consistent Reads (default) - Consistency across all copies of data usually reached within a second. Repeating a read after a short time should return the updated data. (Best Read Performance)
- Strongly Consistent Reads - A Strongly Consistent read returns a result that reflects all writes that received a sucessful response prior to the read.
