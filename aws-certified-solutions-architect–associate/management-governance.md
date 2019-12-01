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

### CloudTrail
AWS CloudTrail increases visibility into your user and resource activity by recording AWS Management Console actions and API calls. You can identify which users and accounts called AWS, the source IP address from which the calls were made, and when the calls occured.

CloudWatch & CloudTrail TL;DR
- CloudWatch monitors performance
- CloudTrail monitors API calls in the AWS platform. CloudTrail is all about auditing.

### AWS CLI
- You can interact with AWS from anywhere in the world just by using the command line (CLI)
- You will need to set up access in IAM
- Commands themselves are not in the exam, but some basic commands will be useful to know for real life
