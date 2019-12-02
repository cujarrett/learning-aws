# Review Questions
A collection of stuff I ran accross that I want to self study with so I remember that content.

---

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

## Storage
What are the two types of distributions in CloudFront?

<details>
<summary>Show answer</summary>
<p>
Web and RTMP

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
