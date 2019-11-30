## Management & Governance

#### CloudWatch
Amazon CloudWatch is a monitoring service to monitor your AWS resources, as well as the applications that you run on AWS.

- CloudWatch monitors performance
- CloudWatch with EC2 will monitor events every 5 minuets by default, but you can run 1 minute intervals by turning on detailed monitoring
- You can create a CloudWatch alarm which trigger notifications
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

#### CloudTrail
AWS CloudTrail increases visibility into your user and resource activity by recording AWS Management Console actions and API calls. You can identify which users and accounts called AWS, the source IP address from which the calls were made, and when the calls occured.

TL;DR
- CloudWatch monitors performance
- CloudTrail monitors API calls in the AWS platform. CloudTrail is all about auditing.
