# Compute

## EC2 (Elastic Compute Cloud)
EC2 is a web service that provides resizeable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minuets, allowing you to quickly scale capacity both up and down, as your computing requirements change.

- Termination Protection is **turned off** by default, you must turn it on
- On an EBS-backed instance, the **default action is for the root EBS volume to be deleted** when the instance is terminated. Any additionaly added volumes won't be deleted.
- EBS Root Volumes of your DEFAULT AMI's **CAN** be encrypted. You can also use a third party tool (such as bit locker etc) to encrypt the root volume, or this can be done when creating AMI's in the AWS console or using the API.
- Additional volumes can be encrypted

### EC2 Pricing Models
1. **On Demand** - Allows you to pay a fixed rate by the hour (or by the second) with no commitment
    - Users that want the low cost and flexibility of Amazon EC2 without any up front payment or long term commitment.
    - Applications with short term, spikey, or upredictable workloads that cannot be interrupted.
    - Applications being developed or tested or Amazon EC2 for the first time
2. **Reserved** - Provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract Terms are 1 year and 3 year terms.
    - Applications with steady state or predictable usage
    - Applications that require reserved capacity
    - Users able to make upfront payments to reduce their total computing costs even further
    - Reserved Pricing Types
      - **Standard Reserved Instances** - These offer up to 75% off on demand instances. The more you pay up front and the longer the contract, the greater the discount.
      - **Convertible Reserved Instances** - These offer up to 54% off on demand capability to change the attributes of the RI as long as the exchange results in the creation of Reserved Instances of equal or greater value. It allows you to change the instance types.
      - **Scheduled Reserved Instances** - These are available to launch within the time windows you reserve. This option allows you to match your capacity reservation to a predictable reoccuring schedule that only requires a fraction of a day, a week, or a month.
3. **Spot** - Enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times. Behaves like the stock market.
    - Applications that have flexible start and end times
    - Applications that are only feasible at very low compute prices
    - Users with urgent computing needs for large amounts of additional capacity
    - If the Spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.
4. **Dedicated Hosts** - Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses.
    - Useful for regulatory requirements that may not support multi-tenant virtualization
    - Great for licensing which does not support multi-tenancy or cloud deployments
    - Can be purchased On-Demand (hourly)
    - Can be purchased as a Reservation for up to 70% off the On-Demand price

### [Security Groups for EC2](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#security-groups)

### Instance Metadata
- Used to get information about an instance (such as public ip)
- `curl http://169.254.169.254/latest/meta-data/` - Shows metadata
- `curl http://169.254.169.254/latest/user-data/` - Shows the bootstap script used to spin up instance

### [EBS (Elastic Block Store)](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#ebs-elastic-block-store)

### [EFS (Elastic File System)](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/storage.md#efs-elastic-file-system)

### EC2 Placement Groups
- The name you specify for a placement group must be unique within your AWS account
- Only certian instances can be launched in a placement group
- You can't merge placement groups
- You can't mive an existing instance into a placement group. You can create an AMI from you existing instance, and then launch a new instance from the AMI into a placement group.

The 3 types of Placement Groups:
1. **Cluster Placement Group**
A Cluster placement Group is a grouping of instances within a single Availability Zone. Placement groups are recomended for applications that need low network latency, high netowrk throughput, or both.
    - A Cluster Placement Group can't span multiple Availability Zones
    - AWS recomended homogenous instanes within Cluster placement Groups (same instance types)

2. **Spread Placement Group**
A Spread Placement Group is a group of instances that are each placed on distinct underlying hardware.
    - Spread Placement Groups are recomended for applications that have a small number of critical instances that should be kept separate from each other.
    - **Think individual instances**
    - Designed to protect your instances from individual failure
    - A Spread Placement Group can span multiple Availability Zones, but they still have to be within the same region

3. **Partitioned Placement Group**
Partitioned Placement Groups divides each group into logical segments called partitions. Amazon EC2 ensures that each partition within a placment group has its own set of racks. Each two partitions within a placement group share the same racks, allowing you to isolate the impact of hardware failure within your application.
    - **Think multiple instances**
    - Could be used in multiple instances of HDFS, HBase, Cassandra
    - A Partitioned Placement Group can span multiple Availability Zones, but they still have to be within the same region

## Elastic Beanstalk
Elastic Beanstalk allows you to quickly deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications. You simply upload your application, and Elastic BeanStalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.

## Compute Review
1. Can Spread Placement Groups be deployed across multiple Availability Zones?
- a. Yes
- b. Only in `Us-East-1`
- c. Yes, but only using AWS CLI
- d. No

<details>
<summary>Show answer</summary>
<p>
- a. Yes

Spread Placement Groups can be deployed across availability zones since they spread the instances further apart. Cluster Placement Groups can only exist in one Availabiity Zone since they are focused on keeping instances together, which you cannot do across Availability Zones
</p>
</details>

2. When creating a new security group, all inbound traffic is allowed by default?
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False
</p>
</details>


2. When creating a new security group, all inbound traffic is allowed by default?
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False

There are slight differences between a normal 'new' Security Group and a 'default' security group in the default VPC. For an 'new' security group nothing is allowed in by default.
</p>
</details>

3. To help you manage your Amazon EC2 instances, you can assign your own metadata in the form of?
- a. Wildcards
- b. Certifcates
- c. Tags
- d. Notes

<details>
<summary>Show answer</summary>
<p>
- c. Tags

Tagging is a key part of managing an environment. Even in a lab, it is easy to lose track of the purpose of a resources, and tricky determine why it was created and if it is still needed. This can rapidly translate into lost time and lost money.
</p>
</details>


4. Which of the following features only relate to Spread Placement Groups?
- a. Instances must be deployed in a single Availability Zone
- b. The name of your placement group must be unique within your AWS account
- c. The placement group can only have 7 running instances per Availability Zone
- d. There is no charge for creating placement group

<details>
<summary>Show answer</summary>
<p>
- c. The placement group can only have 7 running instances per Availability Zone

Spread placement groups have a specific limitation that you can only have a maximum of 7 running instances per Availability Zone and therefore this is the only correct option. Deploying instances in a single Availability Zone is unique to Cluster Placement Groups only and therefore is not correct. The last two remaining options are common to all placement group types and so are not specific to Spread Placement Groups.
</p>
</details>

5. In order to enable encryption at rest using EC2 and Elastic Block Store, you must __________?
- a. Configure encrption when creating the EBS volume
- b. Configure encryption using the appropiate Operating System file system
- c. Configure encruption using X.509 certificates
- d. Mount the EBS volume in to S3 and then encrypt the bucket using a bucket policy

<details>
<summary>Show answer</summary>
<p>
- a. Configure encrption when creating the EBS volume

The use of encryption at rest is default requirement for many industry compliance certifications. Using AWS managed keys to provide EBS encryption at rest is a relatively painless and reliable way to protect assets and demonstrate your professionalism in any commercial situation.
</p>
</details>

6. Can I move a reserved instance from one region to another?
- a. Yes
- b. No
- c. It depends on the region
- d. Only in the US

<details>
<summary>Show answer</summary>
<p>
- b. No

Depending on you type of RL you can You can modify the AZ, scope, network platform, or instance size (within the same instance type), but not Region. In some circumstances you can sell RIs, but only if you have a US bank account.
</p>
</details>

7. You need to know both the private IP and public IP address of your EC2 instance. You should __________?
- a. Run `IPCONFIG` (Windows) or `IFCONFIG` (Linux)
- b. Retrieve the instance Metadata from `http://169.254.169.254/latest/meta-data/`
- c. Retrieve the instance User Data from `http://169.254.169.254/latest/meta-data/`
- d. Use the following command: `AWS EC2 DisplayIP`

<details>
<summary>Show answer</summary>
<p>
- b. Retrieve the instance Metadata from `http://169.254.169.254/latest/meta-data/`

Instance Metadata and User Data can be retrieved from within the instance via a special URL. Similar information can be extracted by using the API via the CLI or an SDK.
</p>
</details>

8. Amazon EBS volumes are __________?
- a. Object-based storage
- b. Block-based storage
- c. Encrypted by default
- d. Not suitable for databases

<details>
<summary>Show answer</summary>
<p>
- b. Block-based storage

EBS, EFS, and FSx are all storage services based on block storage.
</p>
</details>

9. If an Amazon EBS volume is an additional partition (not the root volume) can I detach it without stopping the instance?
- a. Yes, although it may take some time
- b. No, you will need to stop the instance

<details>
<summary>Show answer</summary>
<p>
- a. Yes, although it may take some time
</p>
</details>

10. You can add multiple volumes to an EC2 instance and then create your own RAID 5/RAID 10/RAID 0 configurations using those volumes.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

11. Individual instances are provisioned _____________.
- a. In Regions
- b. In Availability Zones
- c. Globally

<details>
<summary>Show answer</summary>
<p>
- b. In Availability Zones
</p>
</details>

12. Spread Placement Groups can be deployed across multiple Availability Zones.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True

Spread Placement Groups can be deployed across availability zones since they spread the instances further apart. Cluster Placement Groups can only exist in one Availabiity Zone since they are focused on keeping instances together, which you cannot do across Availability Zones
</p>
</details>

13. Is it possible to perform actions on an existing Amazon EBS Snapshot?
- a. Yes, through AWS API's, CLI, and AWS Console
- b. No
- c. It depends on the region
- d. EBS does not have snapshot functionality

<details>
<summary>Show answer</summary>
<p>
- a. Yes, through AWS API's, CLI, and AWS Console
</p>
</details>

14. You have developed a new web application in the US-West-2 Region that requires six Amazon Elastic Compute Cloud (EC2) instances to be running at all times. US-West-2 comprises three Availability Zones (us-west-2a, us-west-2b, and us-west-2c). You need 100 percent fault tolerance: should any single Availability Zone in us-west-2 become unavailable, the application must continue to run. How would you make sure 6 servers are ALWAYS available? NOTE: each answer has 2 possible deployment configurations. Select the answer that gives TWO satisfactory solutions to this scenario.
- a. Solution 1: us-west-2a with two EC2 instances, us-west-2b with two EC2 instances, and us-west-2c with two EC2 instances. Solution 2: us-west-2a with six EC2 instances, us-west-2b with six EC2 instances, and us-west-2c with no EC2 instances.
- b. Solution 1: us-west-2a with six EC2 instances, us-west-2b with six EC2 instances, and us-west-2c with no EC2 instances. Solution 2: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances.
- c. Solution 1: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with no EC2 instances. Solution 2: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances.
- d. Solution 1: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances. Solution 2: us-west-2a with four EC2 instances, us-west-2b with two EC2 instances, and us-west-2c with two EC2 instances.
<details>
<summary>Show answer</summary>
<p>
- b. Solution 1: us-west-2a with six EC2 instances, us-west-2b with six EC2 instances, and us-west-2c with no EC2 instances. Solution 2: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances.

You need to work through each case to find which will provide you with the required number of running instances even if one AZ is lost. Hint: always assume that the AZ you lose is the one with the most instances. Remember that the client has stipulated that they MUST have 100% fault tolerance.
</p>
</details>

15. The use of a cluster placement group is ideal _______.
- a. When you need to distribute content on a CDN network
- b. When you need to deploy EC2 instances that require high disk IO
- c. Your fleet of EC2 instances requires low latency and high network throughput across multiple Availability Zones
- d. Your fleet of EC2 instances requires high network throughput and low latency within a single Availability Zone

<details>
<summary>Show answer</summary>
<p>
- d. Your fleet of EC2 instances requires high network throughput and low latency within a single Availability Zone

Cluster Placement Groups are primarily about keeping you compute resources within one network hop of each other on high speed rack switches. This is only helpful when you have compute loads with network loads that are either very high or very sensitive to latency.
</p>
</details>

16. EBS Snapshots are backed up to S3 in what manner?
- a. Incrementally
- b. Exponentially
- c. Decreasingly
- d. EBS Snapshots are not stored in S3

<details>
<summary>Show answer</summary>
<p>
- a. Incrementally
</p>
</details>

17. Can I delete a snapshot of an EBS Volume that is used as the root device of a registered AMI?
- a. No
- b. Yes
- c. Only via the Command Line
- d. Only using the AWS API

<details>
<summary>Show answer</summary>
<p>
- a. No
</p>
</details>

18. Which AWS CLI command should I use to create a snapshot of an EBS volume?
- a. `aws ec2 create-snapshot`
- b. `aws ec2 fresh-snapshot`
- c. `aws ec2 deploy-snapshot`
- d. `aws ec2 new-snapshot`

<details>
<summary>Show answer</summary>
<p>
- a. `aws ec2 create-snapshot`
</p>
</details>

19. I can change the permissions to a role, even if that role is already assigned to an existing EC2 instance, and these changes will take effect immediately.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

20. To retrieve instance metadata or user data you will need to use the following IP Address:
- a. `http://127.0.0.1`
- b. `http://192.168.0.254`
- c. `http://10.0.0.1`
- d. `http://169.254.169.254`

<details>
<summary>Show answer</summary>
<p>
- d. `http://169.254.169.254`
</p>
</details>

21. Will an Amazon EBS root volume persist independently from the life of the terminated EC2 instance to which it was previously attached? In other words, if I terminated an EC2 instance, would that EBS root volume persist?
- a. Yes
- b. No
- c. Only if I specify (using either the AWS Console or the CLI) that it should be so
- d. It depends on the region in which the EC2 instance is provisioned

<details>
<summary>Show answer</summary>
<p>
- c. Only if I specify (using either the AWS Console or the CLI) that it should be so

You can control whether an EBS root volume is deleted when its associated instance is terminated. The default delete-on-termination behaviour depends on whether the volume is a root volume, or an additional volume. By default, the DeleteOnTermination attribute for root volumes is set to 'true.' However, this attribute may be changed at launch by using either the AWS Console or the command line. For an instance that is already running, the DeleteOnTermination attribute must be changed using the CLI.
</p>
</details>

22. I can use the AWS Console to add a role to an EC2 instance after that instance has been created and powered-up.
- a. True
- d. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

23. Can you attach an EBS volume to more than one EC2 instance at the same time?
- a. No
- d. Yes
- c. If that EC2 volume is part of an AMI
- d. Depends on which region

<details>
<summary>Show answer</summary>
<p>
- a. No
</p>
</details>

24. What are the three types of EC2 Placement Groups?

<details>
<summary>Show answer</summary>
<p>

1. Clustered - for low network latency and or high network throughput
2. Spread - for individual critical EC2 instances
3. Partitioned - for multiple EC2 instances HDFS, HBase, Cassandra

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ec2-placement-groups)
</p>
</details>

25. True or False, a Clustered Placement Group can span multiple Availability Zones?

<details>
<summary>Show answer</summary>
<p>
False

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ec2-placement-groups)
</p>
</details>

26. True or False, a Spread Placement Group and a Partitioned Placement Group can span multiple Availability Zones?

<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#ec2-placement-groups)
</p>
</details>

27. What AWS Compute offering offers quick methods of deploying and managing applications in the AWS Cloud without worrying about the infrastructure that runs those applications.

<details>
<summary>Show answer</summary>
<p>
Elastic BeanStalk, you simply upload your application and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring. 

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/compute.md#elastic-beanstalk)
</p>
</details>
