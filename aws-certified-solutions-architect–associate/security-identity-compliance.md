## Security, Identity & Compliance

### IAM (Identity Access Management)
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
- IAM is Universal, it does not apply to regions at this time

### IAM Key Terminology
1. Users - End Users such as people, employees of an organization etc.
2. Groups - A collection of users. Each user in the group will inherit the permissions of the group.
3. Policies - Policies are made up of documents called Policy documents. These documents are in a format called JSON and they give permissions as to what a User/ Role is able to do.
4. Roles - You create roles and then assign them to AWS Resources.

### CloudWatch
Can be used to create a billing alarm that can send emails or SNS topic when your account goes past the specified amount.

### Security Groups
- Rules changes to Security Groups take effect immediately
- Security Groups are **stateful**. For example, if you allow HTTP traffic in they automatically allow HTTP out.
- You can not blacklist any IP Addresses or ports with Security Groups. Everything is blocked by default and you have to open things. You can use **Network Control Lists** to block IP addresses.
- All inbound traffic is blocked by default
- All outbound traffic is allowed
- You can have any number of EC2 Instances within a security group
- You can have multiple security groups attached to EC2 Instances
- You can specify allow rules but not deny rules

### Users
- New Users have no permissions when first created
- Users can have Access Key ID and Secret Access Key generated for them, these are used to access the AWS API via the AWS CLI. The Access Key ID and Secret Access Key can not be used to log into the AWS Console.

### Roles
- Roles are more secure than storing your access key and secret access key on individual EC2 instances
- Roles are easier to manage
- Roles can be assigned to an EC2 instance after it is created using both the console & command line
- Roles are universal - You can use them in any region

### Review
1. What is an additional way to secure the AWS accounts of both the root account and new users alike?
- a. Implement Mulit-Factor Authentication for all accounts
- b. Store the access key id and secret access key of all users in a publicly accessible plain text document on S3 of which only you and members of your organization know the address.
- c. Configure the AWS Console so that you can only log into it from a specific IP Address range
- d. Configure the AWS Console so that you can only log into it from your internal network IP address range.

<details>
<summary>Show answer</summary>
<p>
- a. Implement Mulit-Factor Authentication for all accounts
</p>
</details>

2. Which of the following is not a component of IAM?
- a. Roles
- b. Users
- c. Groups
- d. Organizational Units

<details>
<summary>Show answer</summary>
<p>
- d. Organizational Units
</p>
</details>

3. When you create a new user, that user __________?
- a. Will be able to log in to the console anywhere in the world, using their access key ID and secret access key
- b. Will be able to interact with AWS using their access key ID and secret access key using the API, CLI, or the AWS SDKs
- c. Will only be able to log into the console in the region in which that user was created
- d. Will be able to log into the console only after multi-factor authentication is enabled on their account.

<details>
<summary>Show answer</summary>
<p>
- b. Will be able to interact with AWS using their access key ID and secret access key using the API, CLI, or the AWS SDKs
</p>
</details>

4. Which statement best describes IAM?
- a. IAM allows you to manage users, groups, roles, and their corresponding level of access to the AWS platform
- b. IAM allows you to managet uses' passwords only. AWS staff must create new users for your organization. This is done by raising a tocket.
- c. IAM allows you to manage permissions for AWS resources only
- d. IAM stands for Improvised Application Management, and it allows you to deploy and manage applications in the AWS Cloud

<details>
<summary>Show answer</summary>
<p>
- a. IAM allows you to manage users, groups, roles, and their corresponding level of access to the AWS platform
</p>
</details>

5. Using SAML (Security Assertion Markup Language 2.0) you can give your federated users single sign-on access to the AWS Management Console.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

6. In what language are policy documents written?
- a. Python
- b. JSON
- c. Node.js
- d. Java

<details>
<summary>Show answer</summary>
<p>
- b. JSON
</p>
</details>

7. What is the default level of access a newly created IAM User is granted?
- a. Read-only access to all AWS services
- b. No access to any AWS services
- c. Administrator access to all AWS services
- d. Power user access to all AWS services

<details>
<summary>Show answer</summary>
<p>
- b. No access to any AWS services
</p>
</details>

8. Which of the following is not a feature of IAM?
- a. IAM offers centralized comntrol of your AWS account
- b. IAM integrates with existing active directory account allowing single sign-on
- c. IAM offers fine grained access of AWS resources
- d. IAM allows you to set up biometric authentication, so that no passwords are required

<details>
<summary>Show answer</summary>
<p>
- d. IAM allows you to set up biometric authentication, so that no passwords are required
</p>
</details>

9. You have a client who is considering a move to AWS. In establishing a new account, what is the first thing the company should do?
- a. Set up an account using Cloud Search
- b. Set up an account using their company email address
- c. Set up an account via SQS (Simple Queue Service)
- d. Set up and account with SNS (Simple Notification Service)

<details>
<summary>Show answer</summary>
<p>
- b. Set up an account using their company email address
</p>
</details>

10. A new employee has just started work, and it is your job to give her administrator access to the AWS console. You have given her a user name, an access key ID, a secret access key, and you have generated a password for her. She is now able to log in to the AWS console, but she is unable to interact with any AWS services. What should you do next?
- a. Grant her Administrator access by adding her to the Administrator's group
- b. Require multi-factor authentication for her user account
- c. Ensure she is logging into the AWS console from your corporate network and not the normal Internet.
- d. Tell her to log out and try logging back in again

<details>
<summary>Show answer</summary>
<p>
- a. Grant her Administrator access by adding her to the Administrator's group
</p>
</details>

11. What level of access does the "root" account have?
- a. Read-only Access
- b. Power User Access
- c. Administrator Access
- d. No Access

<details>
<summary>Show answer</summary>
<p>
- c. Administrator Access
</p>
</details>

12. Power User allows ____________.
- a. Full Access to all AWS services and resources
- b. Read-only access to all AWS services and resources
- c. Access to all AWS services except the management of groups and users within IAM
- d. Users to inspect the source code of the AWS platform

<details>
<summary>Show answer</summary>
<p>
- c. Access to all AWS services except the management of groups and users within IAM
</p>
</details>

13. You are a solutions architect working for a large engineering company that are moving from a legacy infrastructure to AWS. You have configured the company's first AWS account and you have set up IAM. Your company is based in Andorra, but there will be a small subsidiary operating out of South Korea, so that office will need its own AWS environment. Which of the following statements is true?
- a. You will then need to configure Users and Policy Documents for each region, respectively
- b. You will need to configure Users and Policy Documents only once as these are applied globbaly
- c. You will need to configure your users regionally, however your policy documents are global
- d. You will need to configure your policy documents regionally, however your users are global

<details>
<summary>Show answer</summary>
<p>
- b. You will need to configure Users and Policy Documents only once as these are applied globbaly
</p>
</details>

14. You are a security administrator working for a hotel chain. You have a new member of staff who has started as a systems administrator, and she will need full access to the AWS console. You have created the user account and generated the access key id and the secret access key. You have moved this user into the group where the other administrators are, and you have provided the new user with their secret access key and their access key id. However, when she tries to log in to the AWS console, she cannot. Why might that be?
- a. You have not applied the "log in from console" policy document to the user. You must apply this first so that they can log in.
- b. Your user is trying to log in from the AWS Console from outside the corporate network. This is not possible.
- c. You have not yet activated multi-factor authentication for the user, so by default they will not be able to log in
- d. You cannot log in to the AWS Console using the Access Key ID / Secret Access Key pair. Instead, you must generate a password for the user, and supply the user with this password and your organization's unique AWS console login URL.

<details>
<summary>Show answer</summary>
<p>
- d. You cannot log in to the AWS Console using the Access Key ID / Secret Access Key pair. Instead, you must generate a password for the user, and supply the user with this password and your organization's unique AWS console login URL.
</p>
</details>

15. Every user you create in the IAM systems starts with __________.
- a. Full permissions
- b. Partial Permissions
- c. No Permissions

<details>
<summary>Show answer</summary>
<p>
- c. No Permissions
</p>
</details>

16. A ___________ is a document that provides a formal statement of one or more permissions.
- a. Policy
- b. User
- c. Group
- d. Role

<details>
<summary>Show answer</summary>
<p>
- a. Policy
</p>
</details>

17. You have created a new AWS account for your company, and you have also configured multi-factor authentication on the root account. You are about to create your new users. What strategy should you consider in order to ensure that there is good security on this account.
- a. Enact a strong password policy: user passwords must be changed every 45 days, with each password containing a combination of capital letters, lower case letters, numbers, and special symbols.
- b. Require users only to be able to log in using biometric authentication
- c. Restrict login to the corporate network only
- d. Give all users the same password so that if they forget their password they can just ask their co-workers.

<details>
<summary>Show answer</summary>
<p>
- a. Enact a strong password policy: user passwords must be changed every 45 days, with each password containing a combination of capital letters, lower case letters, numbers, and special symbols.
</p>
</details>
