## Storage
#### S3 (Simple Storage Service) provides developers and IT teams with secure durable, highly scalable object storage. Amazon S3 is easy to use, with a simple web service interface to store and retrieve any amount of data from anywhere on the web.

#### What is S3?
- One type of storage in AWS
- S3 is a safe place to store your files
- S3 buckets are PRIVATE by default
- It is Object based storage - meaning you can upload files from 0 Bytes to 5 TB
  - Think of Objects just as files
  - Objects consist of the following:
    - Key - This is the name of the object
    - Value - This is the data and is made up of a sequence of bytes
    - Version ID (Important for versioning)
    - Metadata
    - Subresources
      - Access Control Lists
      - Torrent
- The data is spread across multiple devices and facilities
- Unlimited storage
- Files are stored in Buckets (think of them like folders). S3 is a universal namespace. The Bucket names must be unique globally.
- When you upload a file to S2 you receive a `HTTP 200 code` if the upload was successful
- Because it's object based storage, it's not suitable to install an operating system or database on (for that you'd want block based storage)

#### How does data consistency work for S3?
- Read after Write consistency for PUTS of new Objects
- Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

In other words
- If you write a new file and read it immediately afterwards you will be able to view that data.
- If you update AN EXISTING file or delete a file and read it immediately, you may get the older version, or you may not. Basically the changes to objects take a bit of time to propagate.

#### S3 Guarantees from Amazon
- Built for 99.99% availability for the S3 platform
- Amazon guarantee 99.9% availability
- Amazon guarantee 99.999999999% durability for S3 information (Remember 11 x 9's)

#### S3 Features
- Tiered Storage available
  - **S3 Standard** - 99.99 availability 99.999999999, durability, stored redundantly across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.
  - **S3 IA (Infrequently Accessed)** - For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.
  - **S3 One Zone IA** - For when you want a lower cost option for infrequently accessed data, but do not require the multiple Availability Zone data resilience.
  - **Intelligent Tiering** - Designed to cost optimize costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead. Uses machine learning to automatically move your objects to different Storage Tiers based on use.
  - **S3 Glacier** - S3 Glacier is a secure, durable, and low cost storage class for data archiving. You can reliably store any amount of data at costs that are competitive with or cheaper than on-premises solutions. Retrieval times are configurable from minuets to hours.
  - **S3 Glacier Deep Storage** - S3 Glacier Deep Storage is Amazon S3's lowest cost storage class where a retrieval time of 12 hours is acceptable.

![s3-info](https://user-images.githubusercontent.com/16245634/69601206-07b76200-0fd9-11ea-81d6-9076ba03d117.png)

- Lifecycle Management - ie. When an object is X days old have it on this tier and another tier when it hits Y days old
- Versioning
- Encryption (at rest)
- MFA for Delete optional to safeguard deletes
- Secure your data with **Access Control Lists** and **Bucket Policies**

#### S3 Charges
You are charged for S3 in the following ways:
- Strorage
- Requests
- Storage Management Pricing
- Data Transfer Pricing
- Transfer Acceleration - Enables fast, easy, secure transfers of files over long distances between your end users and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront's globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.
- Cross Region Replication Pricing - Automatic replication to another bucket in a different region

#### Access Control
- Controlling access to S3 can be done using one of the following
  - **bucket ACL**
  - **Bucker Policies**
- S3 buckets are PRIVATE by default. You can setup access control to your buckets using
  - Bucket Policies - Sets access at the bucket level
  - Access Control Lists - Sets access at the individual object level
- S3 buckets can be configured to create access logs which log all requests made to the S3 bucket. This can be sent to another bucket and even another bucket in another account (👀).

#### S3 Encryption
Encryption in Transit is achieved by `SSL`/`TLS`
Encryption at Rest (Server Side) is achieved by
- Server Side
  - **S3 Managed Keys - SSE-S3**
  - **AWS Key Management Service, Managed Keys - SSE-KMS**
  - **Server Side Encryption with Customer Provided Keys - SSE-C**
- Client Side

#### S3 Versioning
- Stores all versions of an object (including all writes and even if you delete an object)
- Great backup tool
- Once enabled, **Versioning cannot be disabled**, only suspended. To remove versioning you'd have to delete the bucket and create a new one.
- Integrates with **Lifecycle** rules
- Versioning's **MFA Delete** capability, which uses multi-factor authentication, can be used to provide an additional layer of security.
- If you have versioning enabled the size of your bucket is the sum of all versions.
- Deleting an object doesn't remove the object but rather places a delete marker over the object in a new version. You can delete the delete marker in that last version to restore the version before it was deleted.

#### S3 Lifecycle Management
- Automates moving your objects between the different storage tiers
- Can be used in conjunction with versioning (but it can work without versioning also)
- Can be applied to current version and if versioning is enabled previous versions

#### S3 Cross Regional Replication
- Versioning must be enabled on both the source and destination bucket
- Regions must be unique
- Existing files in an existing bucket are not replicated automatically. When you add new files they will be then replicated atomically.
- Delete markers are not replicated. This was a deliberate move by AWS to not have deletes auto replicated across all buckets.
- Replication of deleting individual versions of a object (file) will not be replicated

#### Transfer Acceleration
Uses CloudFront Edge network to accelerate your uploads to S3. Instead of uploading directly to your S3 bucket, you can use a distinct URL to upload directly to an Edge Location which will then transfer that file to S3. You will get a distinct URL to upload to. For example: `foo.s3-accelerate.amazonaws.com`.

![aws-s3-transfer-acceleration](https://user-images.githubusercontent.com/16245634/69655407-1125e600-103c-11ea-9091-733833f8a8ad.png)

_image credit www.javatpoint.com_

#### CloudFront
A content delivery network (CDN) is a system of distributed servers (network) that deliver webpages and other content to a user based on the geographic locations of the user, the origin of the webpage, and a content delivery server.

CloudFront can be used to deliver your entire website, including dynamic, static, streaming, and interactive content using a global network of edge locations. Requests for your content are automatically routed to the nearest edge location, so content is delivered with the best possible performance.

- CloudFront is a Networking & Content Delivery solution in AWS
- Edge Locations are not just READ only - you can write to them too (ie put an object on to them as seen in S3 Transfer Acceleration.)
- Objects are cached for the TTL (Time To Live) which is configurable
- You can clear ached objects, but you will be charged. This is called invalidating the cache.
- You can restrict access to content served on CloudFront with signed URL's and or signed cookies

#### CloudFront Terminology
- **Edge Location** - A location where content will be cached. This is separate to an AWS Region/ Availability Zone.
- **Origin** - This is the origin of all files that the CDN will distribute. This can be an S3 Bucket, an EC2 Instance, an Elastic Load Balancer, or Route 53
- **Distribution** - This is the name given to the CDN which consists of a collection of Edge Locations
- **Web Distribution** - Typically used for websites
- **RTMP** - Used for Media Streaming, common with Adobe Flash media streaming

#### Snowball
Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large ammounts of data into and out of AWS. Using Snowball addresses common challenges with large-scale data transfers including high network costs, long transfer times, and security concerns. Transferring data with Snowball is simple, fast, secure, and can be as little as one-fifth the cost of high speed Internet. Once the data transfer job has been processed and verified, AWS performs a software erasure of the Snowball appliance.

- Snowball comes in a 50TB or 80TB size
- Snowball uses multiple layers of security designed to protect your data including
  - Tamper-resistant enclosures
  - 256-bit encryption
  - Industry standard Trusted Platform Module (TPM) designed to ensure both security and full chain of custody of your data.
- Snowball can import to S3
- Snowball can export from S3
  
#### Snowball Edge
Snowball Edge is a 100TB data transfer device with on-board storage and compute capabilities. You can use Snowball Edge to move large ammounts of data into and out of AWS, as a temporary storage tier for large local datasets, or to support local workloads in remote or offline locations. In short it provides temporary storage of large data sets and local workloads in remote or offline locations. You could run AWS Lambda's off of it for example.

Snowball Edge connects to your existing applications and infrastructure using standard storage interfaces, streamlining the data transfer process and minimizing setup and integration. Snowball Edge can cluster together to form a local storage tier and process your data on-premises, helping ensure your applicatons continue to run even when they are not able to access the cloud.

#### Snowmobile
AWS Snowmobile is an Exabyte-scale data transfer service used to move extreamly large amounts of data to AWS. You can transfer up to 100PB per Snowmobile, a 45-foot long ruggedized shipping container, pulled by a semi-trailer truck. Snowmobile makes it easy to move massive volumes of data to the cloud, including video libraries, image repositories, or even complete data center migration. Transfering data with Snowmobile is secure, fast, and cost effective.

#### Storage Gateway
AWS Storage Gateway is a service that connects an on-premises software applicance with cloud-based storage to provide seamless and secure integration between an organization's on-premises IT environment and AWS storage infrastucture. The service enables you to securely store data to the AWS cloud for scalable and cost-effective storage.

Storage Gateway's Software appliance is availablefor download as a virtual machine (VM) image that you install on a host in your datacenter. Storage Gateway supports either VMWare ESXi or Microsoft Hyper-V. Once you've installed your gateway and associated it with your AWS account through the activation process, you can use the AWS Managment Console to create the storage gateway option that is right for you.

![Storage Gateway Diagram](https://user-images.githubusercontent.com/16245634/69677758-4694f880-1069-11ea-8de6-3052e2f7cace.png)

Storage Gateway Types
- File Gateway (NFS & SMB) - Files are stored as objects in your S3 buckets, accessed through a Network File System (NFS) mount point. Ownership, permissions, and timestamps are durably stored in S3 in the user-metadata of the object associated with the file. Once objects are transfered to S3, they can be managed as native S3 objects, and bucket policies such as versioning, lifecycle management, and cross-region replication apply directly to objects stored in your bucket.
- Volume Gateway (iSCSI) - The volume interface presents your applications with disk volumes using the iSCSI block protocol. Data written to these volumes can be asyncchronously backed up as point-in-time shapshots of your volumes, and stored in the cloud as Amazon EBS snapshots. Snapshots are incremental backups that capture only your changed blocks. All snapshot storage is also compressed to minimize your storage charges. There are two types: 
  - Stored Volumes - Enables you to store primary data locally, while asyncchronously backing up that data to AWS. Stored Volumes provide your on-premises applications with low-latency access to their entire adatasets, while providing durable, off-site backups. You can create storage volumes and mount them as iSCSI devices from your on-premises application servers. Data written to your stored volumes is stroed on your on-premises storage hardware. This data is asyncchronously backed up to Amazon S3 in the form of Amazon Elastic Block Stroage (Amazon EBS) snapshots.
  - Cached Volumes -  Enables you to use Amazon S3 as your primary data storage while retaining frequently accessed data locally in your Storage Gateway. Cached volumes minimize the need to scale your on-premises storage infrastructure, while still providing your applications with low-latency access to their frequently accessed data. You can create storage volumes up to 32TiB in size and attach them as iSCSI devices from your on-premises Storage Gateway's cache and upload buffer storage.
- Tape Gateway (VTL) - Offers a durable, cost effective solution to archive your data in the AWS cloud. The VTL interface it provides lets you leverage your existing tape-based backup application infrastructure  to store on virtual tape cartridges that you create on your tape gateway. Each tape gateway is preconfigured with a media changer and tape drivesm which are available to your existing client backup applications as iSCSI devices. You add tape cartridges as you need to archive your data. Supported by NetBackup, Backup Exec, Veeam, etc.

Storage Gateway TL;DR
AWS offers virtual solutions for the following:
- File Gateway - For flat files, stored directly on S3
- Volume Gateway
  - Stored Volumes - Entire dataset is stored on site and is asyncchronously backed up to S3
  - Cached Volumes - Entire dataset is stored on S3 and the most frequently accessed data is cached on site
- Gateway Virtual Tape Library

#### [S3 FAQ](https://aws.amazon.com/s3/faqs/)

### Review
1. What is Amazon Glacier?
- a. A tool that allows you to "freeze" an EBS volume
- b. An AWS service designed for long term data archival
- c. A highly secure firewall designed to keeo everything out
- d. It is a tool used to resurrect deleted EC2 snapshots

<details>
<summary>Show answer</summary>
<p>
- b. An AWS service designed for long term data archival
</p>
</details>

2. You work for a health insurance company that amasses a large number of patients' health records. Each record will be used once when assessing a customer, and will then need to be securely stored for a period of 7 years. In some rare cases, you may need to retrieve this data within 24 hours of a claim being lodged. Given these requirements, which type of AWS storage would deliver the least expensive solution?
- a. S3
- b. S3 - IA
- c. S3 - One Zone - IA
- d. S3 - RRS
- e. Glacier

<details>
<summary>Show answer</summary>
<p>

</p>
</details>
