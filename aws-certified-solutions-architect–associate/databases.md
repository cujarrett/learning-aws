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
