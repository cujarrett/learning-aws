# Review Questions
A collection of stuff I ran accross that I want to self study with so I remember that content.

## Security, Identity & Compliance
Are Roles more or less secure than storing your access key and secret access key on individual EC2 instances?

<details>
<summary>Show answer</summary>
<p>
more

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#roles)
</p>
</details>

True or False, you can assign roles to an EC2 instance both before and after it is created using both the console and command line?

<details>
<summary>Show answer</summary>
<p>
False

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#roles)
</p>
</details>

IAM consists of what?

<details>
<summary>Show answer</summary>
<p>

- Users
- Groups
- Roles
- Policies

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#iam-key-terminology)
</p>
</details>

IAM Policies are stored in what format?

<details>
<summary>Show answer</summary>
<p>
JSON

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#iam-key-terminology)
</p>
</details>

True or False, IAM is universal?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#iam-identity-access-management)
</p>
</details>

True or False, new Users have all permissions when first created?

<details>
<summary>Show answer</summary>
<p>
False, new Users have NO permissions when first created

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#users)
</p>
</details>

True or False, you can use the Access Key ID and Secret Access Key that is created when creating a new User to log into the AWS console.

<details>
<summary>Show answer</summary>
<p>
False, you can not use the Access Key ID and Secret Access Key to log into the AWS Console. You can only use the Access Key ID and Secret Access Key to access the AWS API's via the Command Line.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#users)
</p>
</details>

True or False, you can use IAM to create and customize your own password rotation policies?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#iam-identity-access-management)
</p>
</details>

## Compute
What are the three types of EC2 Placement Groups?

<details>
<summary>Show answer</summary>
<p>

1. Clustered - for low network latency and or high network throughput
2. Spread - for individual critical EC2 instances
3. Partitioned - for multiple EC2 instances HDFS, HBase, Cassandra

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ec2-placement-groups)
</p>
</details>

True or False, a Clustered Placement Group can span multiple Availability Zones?

<details>
<summary>Show answer</summary>
<p>
False

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ec2-placement-groups)
</p>
</details>

True or False, a Spread Placement Group and a Partitioned Placement Group can span multiple Availability Zones?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ec2-placement-groups)
</p>
</details>

## Storage
_________ is Object Based storage?

<details>
<summary>Show answer</summary>
<p>
S3

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-simple-storage-service)
</p>
</details>

True or False, S3 is a universal namespace?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-simple-storage-service)
</p>
</details>

What are the two access control mechanisms for controlling access to S3 buckets?

<details>
<summary>Show answer</summary>
<p>

- Bucket Policies
- Access Control Lists

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-access-control)
</p>
</details>

What are the fundamental parts of S3?

<details>
<summary>Show answer</summary>
<p>

- Key
- Value
- Version ID
- Metadata
- Subresources

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#what-is-s3)
</p>
</details>

What is the consistency model for S3?

<details>
<summary>Show answer</summary>
<p>

- Read After Write consistency for PUTS of new Objects
- Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#how-does-data-consistency-work-for-s3)
</p>
</details>

What are the types of S3?

<details>
<summary>Show answer</summary>
<p>

- S3 Standard
- S3 - IA
- S3 - 1 Zone - IA
- S3 - Intelligent Tiering
- S3 Glacier
- S3 Glacier Deep Archive

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-tiered-storage-options)
</p>
</details>

Encryption In Transit is achieved by?

<details>
<summary>Show answer</summary>
<p>
SSL/TLS

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-encryption)
</p>
</details>

Encryption At Rest is achieved by?

<details>
<summary>Show answer</summary>
<p>

Server Side
- S3 Managed Keys (SSE-S3)
- AWS KMS (Key Management Service) (SSE-KMS)
- Server Side Encryption with Customer Provided Keys (SSE-C)

Client Side Encryption

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-encryption)
</p>
</details>

True or False, for S3 Cross Region Replication, Versioning must be enabled ob both the source and destination buckets??

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-cross-regional-replication)
</p>
</details>

True or False, regions in Cross Region Replication must be unique?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-cross-regional-replication)
</p>
</details>

True or False, Existing files in an S3 bucket are not automatically replicated when you turn on Cross Region Replication?

<details>
<summary>Show answer</summary>
<p>
True, all subsequent updated files will be replicated automatically

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-cross-regional-replication)
</p>
</details>

True or False, with Cross Region Replication, delete markers are not replicated?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-cross-regional-replication)
</p>
</details>

True or False, with Cross Region Replication, deleting individual versions or delete markers will not be replicated?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-cross-regional-replication)
</p>
</details>

What AWS service automates moving your objects between the different S3 tiers??

<details>
<summary>Show answer</summary>
<p>
Lifecycle Management

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-lifecycle-management)
</p>
</details>

True or False, Lifecycle Policies can be used with S3 Versioning?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-lifecycle-management)
</p>
</details>

True or False, Lifecycle Policies can be applied to current versions and previous versions?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#s3-lifecycle-management)
</p>
</details>

What are the two types of distributions in CloudFront?

<details>
<summary>Show answer</summary>
<p>

- Web - Used for websites
- RTMP - Used for media streaming

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#cloudfront)
</p>
</details>

CloudFront origin locations can be what type(s)?

<details>
<summary>Show answer</summary>
<p>

- S3
- EC2 Instance
- ELB (Elastic Load Balancer)
- Route53

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#cloudfront-terminology)
</p>
</details>

True or False, Edge Locations are READ only?

<details>
<summary>Show answer</summary>
<p>
False, you can write to them too (ie put an object on to them)

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#cloudfront)
</p>
</details>

True or False, you can clear cached items in CloudFront?

<details>
<summary>Show answer</summary>
<p>
True, you can invalidate a cached item but you will be charged

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#cloudfront)
</p>
</details>

Instance Store Volumes are sometimes called ______________?

<details>
<summary>Show answer</summary>
<p>
Ephemeral Storage

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#instance-store-volumes)
</p>
</details>

What are the types of AMI storage for the Root Device Volume?

<details>
<summary>Show answer</summary>
<p>
  
- Instance Store Volumes (EPHEMERAL STORAGE)
- EBS Backed Volumes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#instance-store-volumes)
</p>
</details>

Which AMI Root Device Volume type can be stopped without losing data?

<details>
<summary>Show answer</summary>
<p>
EBS backed instances can be stopped. You will not lise the data on this instance if it is stopped. Instance store volumes cannot be stopped. With Instance Store Volumes if the underlying host fails, you will lose your data.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#instance-store-volumes)
</p>
</details>

Which AMI Storage for the Root Device Volume can be rebooted safely without data loss?

<details>
<summary>Show answer</summary>
<p>
You can reboot both Instance Store Volumes (EPHEMERAL STORAGE) and EBS Backed Volumes and you will not lose your data

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#instance-store-volumes)
</p>
</details>

Volumes exist on _________?

<details>
<summary>Show answer</summary>
<p>
EBS, think of EBS as virtual hard disk.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

Snapshots exist on ___________?

<details>
<summary>Show answer</summary>
<p>
S3

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

Snapshots are __________ copies of Volumes.

<details>
<summary>Show answer</summary>
<p>
point in time

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

 Why do initial snapshots take some time to create but subsequent snapshots areq more quick?

<details>
<summary>Show answer</summary>
<p>
Snapshots are incremental - this means that only the blocks that have changed since your last snapshot are moved to S3

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

What can you create AMI's from?

<details>
<summary>Show answer</summary>
<p>
EBS Volume or Snapshots

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

True or False, you can change EBS volume sizes and storage types on the fly?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#ebs-elastic-block-store)
</p>
</details>

True or False, Volumes will always be in the same Availability Zone as the EC2 instance?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

What are the steps to move an EC2 volume from one Availability Zone to another?

<details>
<summary>Show answer</summary>
<p>

1. Take a snapshot
2. Create an AMI from the snapshot
3. Use the AMI to launch the EC2 instance in the new Availability Zone

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#migration)
</p>
</details>

What are the steps to move an EC2 volume from one region to another?

<details>
<summary>Show answer</summary>
<p>

1. Take a snapshot
2. Create an AMI from the snapshot
3. Copy the AMI from the orginal region to the desired region
4. Use the AMI to launch the EC2 instance in the new region

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#migration)
</p>
</details>

True or False, Snapshots of encrypted volumes are encrypted automatically?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

True or False, Volumes restored from encrypted snapshots are encrypted automatically?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#volumes--snapshots)
</p>
</details>

What are the steps to encrypt an unencrypted root device volume that needs to be encrypted?

<details>
<summary>Show answer</summary>
<p>

1. Create a Snapshot of the unencrypted root device volume
2. Create a copy of the Snapshot and select the encrypt option
3. Create an AMI from the encrypted Snapshot
4. Use that AMI to launch new encrypted instances

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#migration)
</p>
</details>

What protocol does EFS support?

<details>
<summary>Show answer</summary>
<p>
Network File System version 4 (NFSv4)

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#efs-elastic-file-system)
</p>
</details>

True or False, with EFS, you only pay for the storage you use?

<details>
<summary>Show answer</summary>
<p>
True, no pre-provisioning required

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#efs-elastic-file-system)
</p>
</details>

True or False, NFS can support thousands of concurrent NFS connections?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#efs-elastic-file-system)
</p>
</details>

True or False, EFS data is stored in a single Availability Zone within a region?

<details>
<summary>Show answer</summary>
<p>
False

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#efs-elastic-file-system)
</p>
</details>

What is the consistency model for EFS?

<details>
<summary>Show answer</summary>
<p>
Read After Write Consistency

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#efs-elastic-file-system)
</p>
</details>

## Management & Governance
What can you use to monitor most of AWS as well as your applications that run on AWS?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

What is the default monitor interval for CloudWatch for EC2?

<details>
<summary>Show answer</summary>
<p>
5 minutes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

What is the detailed monitor interval for CloudWatch for EC2?

<details>
<summary>Show answer</summary>
<p>
1 minutes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

CloudWatch is all about ___________?

<details>
<summary>Show answer</summary>
<p>
Performance

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

CloudTrail is all about ___________?

<details>
<summary>Show answer</summary>
<p>
Auditing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudtrail)
</p>
</details>

In which AWS Service can you create Dashboards?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

In which AWS Service can you create Alarms?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

In which AWS Service can you manage Logs?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

Which AWS service monitors API calls in the AWS platform?

<details>
<summary>Show answer</summary>
<p>
CloudTrail

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudtrail)
</p>
</details>

## Databases
What transactional process is RDS a good choice for?

<details>
<summary>Show answer</summary>
<p>
Online Transactional Processing (OLTP)
</p>
</details>

What is AWS's NOSQL offering?
<details>
<summary>Show answer</summary>
<p>
DynamoDB
</p>
</details>
