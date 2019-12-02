## Matt's Made Up Questions
A collection of stuff I ran accross that I want to self study with so I remember that content.

---

### Storage
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
