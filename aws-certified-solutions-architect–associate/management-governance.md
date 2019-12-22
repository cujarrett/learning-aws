## Management & Governance

### CloudWatch
Amazon CloudWatch is a monitoring service to monitor your AWS resources, as well as the applications that you run on AWS.

- CloudWatch monitors performance
- CloudWatch Standard Monitoring is 5 minute intervals
- CloudWatch Detailed Monitoring is 1 minute intervals
- CloudWatch Dashboards can be global and or regional views to see what is happening with your AWS environment
- CloudWatch Alarms allows you to set Alarms that notify you when particular thresholds are hit
- CloudWatch Events help you respond to state changes in your AWS resources
- CloudWatch Logs helps you aggregate, monitor, and store logs
- CloudWatch can monitor things like
  - Compute
    - EC2 Instances
    - Autoscaling Groups
    - Elastic Load Balancers
    - Route53 Health Checks
  - Storage & Content Delivery
    - EBS Volumes
    - Storage Gateways
    - CloudFront

CloudWatch Host Level Metrics Consist of
- CPU
- Network
- Disk
- Status Check

## CloudTrail
AWS CloudTrail increases visibility into your user and resource activity by recording AWS Management Console actions and API calls. You can identify which users and accounts called AWS, the source IP address from which the calls were made, and when the calls occured.

CloudWatch & CloudTrail TL;DR
- CloudWatch monitors performance
- CloudTrail monitors API calls in the AWS platform. CloudTrail is all about auditing.

## AWS CLI
- You can interact with AWS from anywhere in the world just by using the command line (CLI)
- You will need to set up access in IAM
- Commands themselves are not in the exam, but some basic commands will be useful to know for real life

## CloudFormation
- Is a way of completely scripting your cloud environment
- Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly

### AWS Quick Start
AWS Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly.

## Management & Governance Review

1. What can you use to monitor most of AWS as well as your applications that run on AWS?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

2. What is the default monitor interval for CloudWatch for EC2?

<details>
<summary>Show answer</summary>
<p>
5 minutes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

3. What is the detailed monitor interval for CloudWatch for EC2?

<details>
<summary>Show answer</summary>
<p>
1 minutes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

4. CloudWatch is all about ___________?

<details>
<summary>Show answer</summary>
<p>
Performance

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

5. CloudTrail is all about ___________?

<details>
<summary>Show answer</summary>
<p>
Auditing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudtrail)
</p>
</details>

6. In which AWS Service can you create Dashboards?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

7. In which AWS Service can you create Alarms?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

8. In which AWS Service can you manage Logs?

<details>
<summary>Show answer</summary>
<p>
CloudWatch

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudwatch)
</p>
</details>

9. Which AWS service monitors API calls in the AWS platform?

<details>
<summary>Show answer</summary>
<p>
CloudTrail

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudtrail)
</p>
</details>

10. Which AWS service can be useful for scripting your cloud environment?

<details>
<summary>Show answer</summary>
<p>
CloudFormation

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#cloudformation)
</p>
</details>

11. What is the collection of AWS scripted infrastructure called?

<details>
<summary>Show answer</summary>
<p>
QuickStart, it's bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/management-governance.md#aws-quick-start)
</p>
</details>
