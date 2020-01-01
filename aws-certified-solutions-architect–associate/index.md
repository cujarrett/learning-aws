## What?
I'd like to pass the [AWS Certified Solutions Arch](Associatehttps://aws.amazon.com/certification/certified-solutions-architect-associate/)

## Tasks
- [x] - [Ryan Kroonenburg's AWS Certified Solutions Arch Associate course](https://www.udemy.com/course/aws-certified-solutions-architect-associate/)
- [ ] - [Review Longest Prefix Match Understanding Advanced Concepts in VPC Peering](https://tutorialsdojo.com/longest-prefix-match-understanding-advanced-concepts-in-vpc-peering/)
- [ ] - [Jon Bonso's AWS Certified Solutions Architect Associate Practice Exams](https://www.udemy.com/course/aws-certified-solutions-architect-associate-amazon-practice-exams/)
- [ ] - [Skillcertpro's AWS Certified Solutions Architect 2019 Practice Questions](https://www.udemy.com/course/aws-certified-solutions-architect-2018-practice-questions/)
- [ ] - Take AWS Certified Solutions Arch Associate exam
- [ ] - [Celebratory Dance](https://media.giphy.com/media/6fScAIQR0P0xW/giphy.gif)

#### Notes Preface
I am going to focus on probable elements in the exam to streamline note taking. For example I will detail difference between a Regions and an Availability Zone but I won't take notes on current number of each as it's not as important and in constant change.

## AWS Topics Studied
Bold topics are core services and very important to know well
- [x] - [**AWS Global Infrastructure**](./aws-global-infrastructure.md)
- [x] - [**Security, Identity & Compliance**](security-identity-compliance.md)
- [x] - [**Compute**](./compute.md)
- [x] - [**Storage**](./storage.md)
- [x] - [**Databases**](./databases.md)
- [x] - [**Network & Content Delivery**](./network-content-delivery.md)
- [x] - [Application Integration](./application-integration.md)
- [x] - [Management & Governance](./management-governance.md)
- [x] - [Analytics](./analytics.md)
- [x] - [Media Services](./media-services.md)

## Things I like
- Elastic nature of AWS
- Resources spin up in seconds versus days/weeks/months to order new hardware
- Becuase it's so easy to spin up and spin down resources, it enables more expirmentation to best meet customers and business needs vs putting a lot of eggs in one basket and hoping you designed it right

## Things I don't like
- Most solutions require setting up of many things like Roles, API Gateway, etc and you have spin each down seperattly. I understand why this is and can even excuse it for most things but the Elastic Beanstalk should orchistrate spinning down everything it automatically spins up. TL;DR if you can spin up X or Y with a single click, you should be able to spin down X or Y with the same single click.
- It's probbaly just me but I wish I there more of a link between what you're being billed for and the AWS resources that are running. `EC2-Other` isn't very clear.
- Inconsitency from one AWS service to another. Small example would be to delete a resource you see all of these type the fill name of the bucket to delte it, type Confirm, type confirm, type Delete, etc
- When new AWS services are launched the the search results are quickly outdated leading to time waste IMO
