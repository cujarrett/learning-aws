## Security, Identity & Compliance

#### IAM (Identity Access Management)
IAM allows you to mange users and their level of access to the AWS Console. It is Global, as in it does not apply to a specific AWS Region but rather all AWS Regions for your account. The "root account" is simply the account created when you first set up your AWS account. It has complete Admin access. New Users have **no** permissions when first created. New Users can be assigned **Access Key ID** & **Secret Access Keys** when first created (used for programmatic access to AWS resources). Users can have access to AWS Console and or programatic access. Always use Multifactor Authentication on your root account (It's 2019, MFA all the things). You can create and customize password rotation policies.

IAM Features
- Centralized control of your AWS account
- Shared Access to your AWS account
- Granular Permissions
- Identity Federation (including Active Directory, FaceBook, Linkedin, etc)
- Multifactor Authentication
- Provides temporary access for users/ devices and services where necessary
- Allows you to set up your own password rotation policy
- Provides PCI DSS Compliance

#### IAM Key Terminology
1. Users - End Users such as people, employees of an organization etc.
2. Groups - A collection of users. Each user in the group will inherit the permissions of the group.
3. Policies - Policies are made up of documents called Policy documents. These documents are in a format called JSON and they give permissions as to what a User/ Role is able to do.
4. Roles - You create roles and then assign them to AWS Resources.

#### CloudWatch
Can be used to create a billing alarm that can send emails or SNS topic when your account goes past the specified amount.
