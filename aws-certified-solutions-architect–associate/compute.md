## Compute

#### EC2 (Elastic Compute Cloud) is a web service that provides resizeable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minuets, allowing you to quickly scale capacity both up and down, as your computing requirements change.

- Termination Protection is **turned off** by default, you must turn it on
- On an EBS-backed instance, the **default action is for the root EBS volume to be deleted** when the instance is terminated. Any additionaly added volumes won't be deleted.
- EBS Root Volumes of your DEFAULT AMI's **CAN** be encrypted. You can also use a third party tool (such as bit locker etc) to encrypt the root volume, or this can be done when creating AMI's in the AWS console or using the API.
- Additional volumes can be encrypted

#### EC2 Pricing Models
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
    
    #### [Security Groups](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/security-identity-compliance.md#security-groups)

#### EBS (Elastic Block Store)
Elastic Block Store provides persistent block storage volumes for use with Amazon EC2 instances in the AWS Cloud. Each Amazon EBS volume is automatically replicated within its Availability Zone to protect you from component failure, offering high availability and durability.

- When adding additional volumes `Delete on Termination` is not checked automatically
- You can change the type of EBS that the bootable OS is on to **Provisioned IOPS** (**io1**) without having downtime (crazy cool tech).
- You can change EBS volume sizes and storage types on the fly

#### 5 Different EBS Storage Types
- **General Purpose** (**gp2**) (SSD) - General purpose SSD volume that balances price and performance for a wide variety of transactional workloads
- **Provisioned IOPS** (**io1**) (SSD) - Really fast input/outputs per second. Highest performing SSD volume designed for mission-critical applications.
- **Throughput Optimised Hard Disk Drive** (**st1**) - Low cost HDD volume designed for frequently accessed, throughput intensive workloads
- **Cold Hard Disk Drive** (**sc1**) - Lowest cost HDD volume designed for less frequently accessed workloads
- **Magnetic** (**Standard**) - Previous generation HDD

![ebs-info](https://user-images.githubusercontent.com/16245634/69844985-3bda8f00-1234-11ea-9736-f6b99fd13ef6.png)

#### Volumes & Snapshots
- Volumes will ALWAYS be in the same Availability Zone as the EC2 instance
- AMI (Amazon Machine Image) provides the information required to launch an instance
- Volumes exist on EBS. Think of EBS as virtual hard disk in the cloud.
- Snapshots exist on S3. Think of snapshots as a photograph of the disk.
- Snapshots are point in time copies of Volumes.
- Snapshots are incremental - this means that only the blocks that have changed since your last snapshot are moved to S3
- If this is your first snapshot, it may take some time to create
- To create a snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot. However, you can take a snapshot of the instance while running.
- You can create AMI's from both volumes and Snapshots

#### Migration
To move an EC2 volume from one Availability Zone to another:
1. Take a snapshot of it
2. create an AMI from the snapshot
3. Use the AMI to launch the EC2 instance in a new Availability Zone

To move an EC2 volume from one region to another:
1. Take a snapshot of the volume
2. Create an AMI from the snapshot
3. Copy the AMI from one region to the other
4. Use the copied AMI to launch the new EC2 instance in the new region

#### AMI Types
- Region
- Operating System
- Architecture (32 bit or 64 bit)
- Launch Permissions
- Storage for the Root Device Volume
  - Instance Store (EPHEMERAL STORAGE)
  - EBS Backed Volumes

#### EBS vs Instance Store Volumes
- All AMIs are categorized as either backed by Amazon EBS or backed by instance store
- **For EBS Volumes**: The root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot
- **For Instance Store Volumes**: The root device for an instance from the AMI is an instance store volume created from a template stored in Amazon S3
- Instance Store Volumes are sometimes called Ephemeral Storage
- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.
- EBS backed instances can be stopped. You will not lise the data on this instance if it is stopped.
- You can reboot both, you will not lose your data
- By default, both ROOT volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume.
