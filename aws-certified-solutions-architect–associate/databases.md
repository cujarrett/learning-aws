## Databases

#### Relational Database
A Relational Database are what most of us are all used to. They have been around since the 70's. Think of a traditional spreadsheet.
- Databases
- Tables
- Row
- Fields

### AWS RDS (Relational Database Service)
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

#### Non Relational Database
- Collection = Table
- Document = Row
- Key Value Pair = Fields

AWS Non Relational Database Offerings
  - DynamoDB (NOSQL)

### Data Warehousing
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
### ElastiCache
ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

- Used to speed up performance of an existing databases (frequent identical queries)

AWS ElastiCache supports two open-source in-memory caching engines
  - Memcached
  - Redis

### Backups With RDS
- **Automated Backups** - Allow you to recover your database to any point in time within a retention period. The retention period can be between 1 and 35 days. Automated Backups will take a full daily snapshot and will also store transactional logs throughout the day. When you do a recovery, AWS will first choose the most recent daily backup, and then apply transactional logs relevent to that day. This allows you to do point in time recovery down to a second, within the retention period.

  Automated Backups are enabled by default. The backup data is stored in S3 and you get free storage equal to the size of your database. So if you have an RDS instance of 10Gb, you will get 10Gb worth of storage.

  Backups are taken within a defined maintenance window. During the backup window, storage I/O may be suspended while your data is being backed up and you may expereince elevated latency.
  
- **Database Snapshots** - Done manually, (ie they are user intiated). They are stored even after you delete the orginal RDS instance, unlike automated backups.

### Restoring Backups With RDS
Whenever you restore either an Automated Backup or Snapshot Backup, the restored verson of the database will be a new RDS instance with a new DNS endpoint.

![backups-get-a-new-dns-endpoint](https://user-images.githubusercontent.com/16245634/70203166-a599e380-16e1-11ea-9f88-52a76e175825.png)

__image from [A Cloud Guru](https://acloud.guru/)

### RDS Encryption At Rest
Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB, Aurora. Encryption is done using the AWS Key Management Service (KMS). Once your RDS instance is encrypted, as are its backups, read replicas, and snapshots.

Encryption at rest is available for the following RDS database types:
- MySQL
- Oracle
- SQL Server
- PostgreSQL
- MariaDB
- Aurora

#### RDS Multi-AZ (Multiple Availability Zone)
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
