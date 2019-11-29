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

#### 5 Different EBS Storage Types
- **General Purpose** (**gp2**) (SSD) - General purpose SSD volume that balances price and performance for a wide variety of transactional workloads
- **Provisioned IOPS** (**io1**) (SSD) - Really fast input/outputs per second. Highest performing SSD volume designed for mission-critical applications.
- **Throughput Optimised Hard Disk Drive** (**st1**) - Low cost HDD volume designed for frequently accessed, throughput intensive workloads
- **Cold Hard Disk Drive** (**sc1**) - Lowest cost HDD volume designed for less frequently accessed workloads
- **Magnetic** (**Standard**) - Previous generation HDD

![ebs-info](https://user-images.githubusercontent.com/16245634/69844985-3bda8f00-1234-11ea-9736-f6b99fd13ef6.png)
