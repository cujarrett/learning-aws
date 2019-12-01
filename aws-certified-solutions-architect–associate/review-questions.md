## Matt's Made Up Questions
A collection of stuff I ran accross that I want to self study with so I remember that content.

---

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

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ebs-vs-instance-store-volumes)
</p>
</details>

What are the types of AMI storage for the Root Device Volume?

<details>
<summary>Show answer</summary>
<p>
- Instance Store (EPHEMERAL STORAGE)
- EBS Backed Volumes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ami-types)
</p>
</details>

Which AMI Root Device Volume type can be stopped without losing data?

<details>
<summary>Show answer</summary>
<p>
Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ami-types)
</p>
</details>

Which AMI Storage for the Root Device Volume can be rebooted safely without data loss?

<details>
<summary>Show answer</summary>
<p>
You can reboot both Instance Store (EPHEMERAL STORAGE) and EBS Backed Volumes and you will not lose your data

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ami-types)
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
