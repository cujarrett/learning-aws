# Network Content Delivery

## DNS
DNS is used to convert human friendly domain names such as https://acloud.guru into an Internet Protocol (IP) address such as http://82.124.53.1. IP addresses are used by computers to identify each other on the network. IP addresses commonly come in 2 different forms, IPv4 and IPv6.

![DNS Example](https://user-images.githubusercontent.com/16245634/70384081-cca12100-193e-11ea-8ae5-4df3c715248a.png)
_image from [A Cloud Guru](https://acloud.guru/)_

## IPv4 vs IPv6
The IPv4 space is a 32 bit field and has over 4 billion different addresses (4,294,967,296 to be precise).

IPv6 was created to solve this depletion issue ad has an address space of 128 bits which in theory is 340,282,366,920,938,463,463,374,607,431,768,211,456 addresses or 340 undecillion addresses.

## Top Level Domain vs Second Level Domain
The last part of the URL is called a Top Level Domain. The second word in the URL is the Second Level Domain. For example: www.foo.co.uk where `co` is Second Level Domain and `uk` is the Top Level Domain.

Top Level Domain names are controlled by the Internet Assigned Numbers Authority (IANA) in a root zone database by visiting http://www.iana.org/domains/root/db

Becuase all of the names in a given domain name have to be unique there needs to be a way to organize this all so that domain names aren't duplicated. This is where domain registars come in. A registar is an authority that can assign domain names directly under one or more top-level domains. These domains are registered with the InterNIC, a service of ICANN, which enforces uniqueness of domain names across the internet. Each domain name becomes registered in a central database known as the WhoIS database. Popular domain registars include: Amazon, Google, GoDaddy.com, 123-reg.co.uk etc.

## Common DNS Types
- ### SOA (Start of Authority Record)
  The SOA stores info about:
  - The name of the server that supplied the data for the zone
  - The administrator of the zone
  - The current version of the data file
  - The default number of seconds for the time to live file on resource records
    
- ### NS (Name Server Records)
  They are used by Top Level Domain servers to direct traffic to the Content DNS server which contains the authoritative DNS records.

- ### A Record
    An "A" Record is the fundamental type of DNS record. The "A" in A Record stands for "Address". The A Record is used by a computer to translate the name of the domain to an IP address. For example, http://www.acloud.guru might point to http://123.10.10.80.

- ### CName
  A Canonical Name (CName) can be used to resolve one domain name to another. For example, you may have a mobile website with the domain name http://m.acloud.guru that is used for when users browse to your domain name on their mobile devices. You may also want the name http://mobile.acloud.guru to resolve to this same address.

- ### MX Records
- ### PTR Records

## TTL (Time to Live)
TTL is the length that a DNS record is cached on either the Resolving Server or the users own local PC is equal to the value of the "Time To Live" (TTL) in seconds. The lower the time to live, the faster changes to DNS records take to propagate throughout the internet.

## Alias Records
Alias Records are used to map resource record sets in your hosted zone to Elastic Load Balancers, CloudFront, CloudFront distributions, or S3 buckets that are configured as websites.

Alias Records work like a CName record in that you can map one DNS name (www.example.com) to another "target" DNS name (elb1234.elb.amazonaws.com).

Key difference, A CName can't be used for naked domain names (zone apex record). You can't have a CName for http://acloud.guru, it must be either a A Record or and Alias.

## Route 53
Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Amazon Route 53 is fully compliant with IPv6 as well.

Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints. Amazon Route 53 Traffic Flow makes it easy for you to manage traffic globally through a variety of routing types, including Latency Based Routing, Geo DNS, Geoproximity, and Weighted Round Robin—all of which can be combined with DNS Failover in order to enable a variety of low-latency, fault-tolerant architectures. Using Amazon Route 53 Traffic Flow’s simple visual editor, you can easily manage how your end-users are routed to your application’s endpoints—whether in a single AWS region or distributed around the globe. Amazon Route 53 also offers Domain Name Registration – you can purchase and manage domain names such as example.com and Amazon Route 53 will automatically configure DNS settings for your domains.

- You can buy domain names directly with AWS
- It can take up to 3 days to register depending on the circumstances
- ELBs do not have pre-defined IPv4 addresses; you resolve to them using a DNS name
- Understand the difference between an ALias Record and a CName
- Given the choice, always choose an Alias Record over a CName

### Route 53 Routing Policies
- #### Simple Routing
  ![Simple Routing example](https://user-images.githubusercontent.com/16245634/70397187-b09c8e80-19d5-11ea-8b76-c3261956393a.png)
  _image from [A Cloud Guru](https://acloud.guru/)_
  
  If you choose the Simple Routing Policy you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route 53 returns all values to the user in a random order.
  - You can not have a health check with a Simple Routing. Consider Multivalue Answer Routing for a good option similar to Simple Routing.

- #### Weighted Routing
  ![Weighted Routing example](https://user-images.githubusercontent.com/16245634/70397476-2e619980-19d8-11ea-8291-f99f8a820976.png)
  _image from [A Cloud Guru](https://acloud.guru/)_
  
  Allows you to split your traffic based on different weights assigned. For example, you can set 10% of your traffic to go to `US-EAST-1` and 90% to go to `EU-WEST-1`.

- #### Latency-based Routing
  ![Latency-based Routing example](https://user-images.githubusercontent.com/16245634/70398028-d2e5da80-19dc-11ea-941f-c48c65efb696.png)
  _image from [A Cloud Guru](https://acloud.guru/)_
  
  Latency-based Routing allows you to route your traffic based on the lowest network latency for your end user (ie which region will give them the fastest response time).
  
  To use Latency-based Routing, you create a latency resource record set for the Amazon EC2 (or ELB) resource in each region that hosts your website. When AmazonRoute 53 receives a query for your site, it selects the latency resource record set for the region that gives the lowest latency. Route 53 then responds with the value associated with that resource record set.

- ##### Failover Routing
  ![Failover Routing example](https://user-images.githubusercontent.com/16245634/70398195-8a2f2100-19de-11ea-9db7-3c839296ee59.png)
  _image from [A Cloud Guru](https://acloud.guru/)_
  
  Failover Routing policies are used when you want to create an activity/ passive set up. For example, you may want your primary site in `EU-WEST-2` and your secondary DR site in `AP-SOUTHEAST-2`.

  Route 53 will monitor the health of your primary site using a health check.

  A health check monitors the health of your end points.

- ##### Geolocation Routing
  ![Geolocational Routing example](https://user-images.githubusercontent.com/16245634/70398395-88fef380-19e0-11ea-86ff-f069ce9678ab.png)
  _image from [A Cloud Guru](https://acloud.guru/)_
  
  Geolocation Routing lets you choose where your traffic will be sent based on the geographic location of your users (ie the location from which DNS queries originate). For example, you may want all queries from Europe to be routed to a fleet of EC2 instanes that are specifically configured for your European customers. These servers may have the local language of your European customers and all prices are displayed in Euros.

- ##### Geoproximity Routing (Traffic Flow Only)
  Geoproximity Routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and  your resources. You can also optionally choose to route more traffic or less traffic to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.
  
  - Geolocation Routing does not factor in latency, it only factors in request location
  - To use Geoproximity Routing, you must use Route 53 Traffic Flow

- ##### Multivalue Answer Routing
  Multivalue Answer Routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record, but Multivalue Answer Routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources.
  
  **This is similar to Simple Routing however it allows you to put health checks on each record set.**

### Route 53 Health Checks
- You can set health checks on individual recordds sets
- If a record set fails a health check it will be removed from Route53 until it passes the health 
- You can set SNS notifications to alert you if a health check is failed

## VPC (Virtual Private Cloud)
Amazon Virtual Cloud (Amazon VPC) lets you provision a logically isolated section of the Amazon Web Services (AWS) Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

You can easily customize the network configuration for your Amazon Virtual Private Cloud. For example, you can create a public facing subnet for your webservers that has access to the Internet, and place your backend systems such as databases or application servers in a private-facing subnet with no Internet access. You can leverage multiple layers of security, including security groups and network access control lists, to help control access to Amazon EC2 instances in each subnet.

Additionaly, youo can create a Hardware Virtual Private Network (VPN) connection between your corporate datacenter and your VPC and leverage the AWS cloud as an extension of your corporate datacenter.

- Think of a VPC as a virtual data center in the cloud.
- Consists of IGWs (or Virtual Private Gateways), Route Tables, Network Access Control Lists, Subnets, Security Groups
- 1 Subnet = 1 Availability Zone
- Security Groups are Stateful; Network Access Control Lists are Stateless
- NO TRANSITIVE PEERING
- When you create a VPC a default Route Table, Network Access Control List (NACL) and a default Security Group
- It won't create any subnets, nor will it create a default Internet gateway
- `US-East-1A` in your AWS account can be a complettly different availability Zone to `US-East-1A` in another AWS account. The Availability Zones are randominzed.
- Amazon always reserves 5 IP addresses within your subnets
- You can only have 1 Internet Gateway per VPC
- Security Groups can't span VPCs

![VPC Diagram](https://user-images.githubusercontent.com/16245634/70491350-b3c37780-1ac6-11ea-9d84-e2b9676b1c8d.png)
_image from [A Cloud Guru](https://acloud.guru/)_

### VPC Features
- Launch instances into a subnet of your choosing
- Assign custom IP address ranges in each subnet
- Configure route tables between subnets
- Create Internet gateway and attach it to our VPC
- Much better security control over your AWS resources
- Instance security Groups
- Subnet network access control lists (ACLS)

### Default VPC vs Custom VPC
- Default VPC is user friendly, allowing you to immediately deploy instances
- All subnets in default VPC have a route out to the Internet
- Each EC2 instance has both a public and private IP address

### VPC Peering
- Allows you to connect one VPC to another via a direct network route using private IP addresses
- Instance behave as if they were on the same private network
- You can peer VPC's with other AWS accounts as well as with other VPCs in the same account
- Peering is in a star configuration: ie 1 central VPC peers with 4 others. NO TRANSITIVE PEERING!

### VPC Flow Logs
VPC FLow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow Log data is stored using Amazon CloudWatch Logs. After you've created a flow log, you can view and retrieve its data in Amazon CloudWatch Logs.

- You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account
- You cannot tag a flow log
- After you've created a flow log, you cannot change its configurationl for example, you can't associate a different IAM role with the flow log
- Not all IP traffic is monitored
  - Traffic generated by instances when they contact the Amazon DNS server it won't be monitored. If you own your own DNS server, then all traffic to that DNS server is logged.
  - Traffic generated by a Windows intance for Amazon Windows license activation will not be monitored
  - Traffic to and from 169.254.169.254 for instance metadata won't be monitored
  - DHCP traffic is not monitored
  - Traffic to the reserved IP address for the default VPC router is not monitored

#### VPC Flow Log Levels:
- VPC
- Subnet
- Network Interface Level

### VPC Endpoint
A VPC Endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an Internet Gateway, NAT Device, VPM Connection, or AWS Direct Connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.

Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.

#### Two Types of VPC Endpoints
- **Interface Endpoints** - an elastic network interface with a private IP address that serves as an entry point for traffic destined to a support service. The following services are supported:
- **Gateway Endpoints** - Supported for Dynamo DB and S3 currently

## Network Access Control Lists
- Your VPC automatically comes with a default network ACL, and by default it allows all traffic outbound and inbound traffic.
- You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.
- Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
- Block IP Addresses using network ACLs not Security Groups
- You can associate a network ACL with multiple subnets; however a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
- Network ACLs contain a numbered list of rules that is evualated in order, starting with the lowest numbered rule
- Network ACLs have seperate inbound and outbound rules, and each rule can either allow or deny traffic
- Network ACLs are stateless; responsees to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa)

## NAT Instances
- When creating a NAT instance, Disable Source and Destination Checks on the instance
- NAT instances myst be in a public subnet
- There must be a route out of the private subnet to the NAT instance, in order for this to work
- The ammount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size
- You can create high availability using Autoscaling Groups, multiple subnets in different Availability Zones, and script to automate failover
- Behind a Security Group

## NAT Gateways
- Redundant inside the Availability Zone
- Prefered for enterprise use
- You can only have one NAT Gateway innside one Availability Zone, NAT Gateways can not span Availability Zones
- Starts at 5Gbs and scales currently to 45Gbs (You won't be tested on this)
- No need to patch
- Not associated with Security Groups
- Automatically assigned a public IP address
- Remember to update your route tables
- No need to disable Source and Destination Checks
- If you have resources in multiple Availability Zones and they share one NAT Gateway, in the event that the NAT Gateway's Availability Zone is down, resources in the other Availability Zones lose internet access. To create an Availability Zone independent architecture, create a NAT gateway in each Availability Zone and configure your routing to ensure that resources use the NAT Gateway in the same Availability Zone.

## Bastion Host
A Bastion Host is a special computer on a network specifically designed and configured to withstand attacks. The computer generally hosts a single application, for example a proxy server, and all other services are removed or limited to reduce the threat to the computer. It is hardened in this manner primarily due to its location and purpose, which is either on the outside of the firewall or in a demilitarized zone (DMZ) and usually involves access from untrusted networks or computers.

- A NAT Gateway or NAT Instance is used to provide Internet traffic to EC2 instances in a private subnets
- A Bastion Host is used to securely administer EC2 instances (using SSH or RDP). Bastions are called Jump Boxes in Australia.
- You cannot use a NATE Gateway as a Bastion Host

## Direct Connect
AWS Direct Connect is a cloud service solution that makes it easy to estabilish a dedicated network connection from your premises to AWS. Using AWS Direct Connectm you can estabilish private connectivity between AWS and your datacenter, office, colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet based connections.

![Direct Connect diagram](https://user-images.githubusercontent.com/16245634/70855101-b0dfd280-1e8a-11ea-94a1-5f9e5db27450.png)
_image from [A Cloud Guru](https://acloud.guru/)_

- Direct Connect directly connects your data center to AWS
- Useful for high throughput workloads (ie lots of network traffic)
- Useful if you need a stable and reliable secure connection

## Network Content Delivery Review
1. Which of the following Route 53 policies allow you to a) route data to a second resource if the first is unhealthy, and b) route data to resources that have better performance?
- a. Failover and Simple Routing
- b. Geoproximity Routing and Geolocational Routing
- c. Geolocational Routing and Latency-based Routing
- d. Failover Routing and Latency-based Routing

<details>
<summary>Show answer</summary>
<p>
- d. Failover Routing and Latency-based Routing

Failover Routing and Latency-based Routing are the only two correct options, as they consider routing data based on whether the resource is healthy or whether one set of resources is more performant than another. Any answer containing location based routing (Geoproximity and Geolocation) cannot be correct in this case, as these types only consider where the client or resources are located before routing the data. They do not take into account whether a resource is online or slow. Simple Routing can also be discounted as it does not take into account the state of the resources.
</p>
</details>

2. Route 53 is Amazon's DNS Service.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

3. Route 53 is named so because ________.
- a. It was invented in 1953
- b. Route 66 was already registered with Microsoft
- c. The DNS port is on port 53 and Route 53 is a DNS Service
- d. Beats me - only people in marketing can tell you the reason behind its name

<details>
<summary>Show answer</summary>
<p>
- c. The DNS port is on port 53 and Route 53 is a DNS Service
</p>
</details>

4. You have created a new subdomain for your popular website, and you need this subdomain to point to an Elastic Load Balancer using Route53. Which DNS record set should you create?
- a. A
- b. AAAA
- c. MX
- d. CName

<details>
<summary>Show answer</summary>
<p>
- d. CName
</p>
</details>

5. True or False: There is a limit to the number of domain names that you can manage using Route 53.
- a. True. There is a hard limit of 100 domain names. You cannot go above this number.
- b. True and False. With Route 53, there is a default limit of 50 domain names. However, this limit can be increased by contacting AWS support.
- c. False. By default, you can support as many domain names on ROute 53 as you want.

<details>
<summary>Show answer</summary>
<p>
- b. True and False. With Route 53, there is a default limit of 50 domain names. However, this limit can be increased by contacting AWS support.
</p>
</details>

6. You are hosting a website and would like visitors from United Kingdom to see a different site than those in Australia. Which Routing Policy would help you to accomplish this?
- a. Failover Routing policy
- b. Geolocation Routing policy
- c. Geoproximity Routing policy
- d. Latency Routing policy

<details>
<summary>Show answer</summary>
<p>
- b. Geolocation Routing policy

Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region.
</p>
</details>

7. Your company hosts 10 web servers all serving the same web content in AWS. They want Route 53 to serve traffic to random web servers. Which routing policy will meet this requirement, and provide the best resiliency?
- a. Simple Routing
- b. Weighted Routing
- c. Multivalue Routing
- d. Latency-based Routing

<details>
<summary>Show answer</summary>
<p>
- c. Multivalue Routing

Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. Route 53 responds to DNS queries with up to eight healthy records and gives different answers to different DNS resolvers. The choice of which to use is left to the requesting service effectively creating a form or randomization.
</p>
</details>

8. Do ELB's have pre-defined IPv4 addresses?
<details>
<summary>Show answer</summary>
<p>
No, you resolve to them using a DNS name.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#route-53)
</p>
</details>

9. What is the difference between a Alias Record and a CName?
<details>
<summary>Show answer</summary>
<p>
Think of the Alias Address as a phone book where Bruce Wayne's phone number 123-456-7890 and a CName would say Batman, see Bruce Wayne.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#common-dns-types)
</p>
</details>

10. Given the choice of CName and Alias Record, which should you always choose?
<details>
<summary>Show answer</summary>
<p>
Alias Record

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#route-53)
</p>
</details>

11. What are the common DNS types?
<details>
<summary>Show answer</summary>
<p>

- SOA Record
- NS Record
- A Record
- CName
- MX Records
- PTR Records

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#common-dns-types)
</p>
</details>

12. What are the routing policies available with Route 53?
<details>
<summary>Show answer</summary>
<p>

- Simple Routing
- Weighted Routing
- Latency-based Routing
- Failover Routing
- Geolocation Routing
- Geoproximity Routing (Traffic Flow Only)
- Multivalue Answer Routing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#route-53-routing-policies)
</p>
</details>

13.What can you set Route 53 health checks on?
<details>
<summary>Show answer</summary>
<p>
Individual record sets

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#route-53-health-checks)
</p>
</details>

14. What happens if a record set fails a health check?
<details>
<summary>Show answer</summary>
<p>
It will be removed until it passes the health check

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#route-53-health-checks)
</p>
</details>

15. How can you stay informed of a failing health check?
<details>
<summary>Show answer</summary>
<p>
You can set up SNS notifications to alert you if a health check is failed

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#route-53-health-checks)
</p>
</details>

16. If you choose a Simple Routing policy, how many records can you have with multiple IP addresses?
<details>
<summary>Show answer</summary>
<p>
1

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#simple-routing)
</p>
</details>

17. If you specify multiple values in a Simple Routing policy record how will Route 53 choose which node to send the traffic?
<details>
<summary>Show answer</summary>
<p>
Random

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#simple-routing)
</p>
</details>

18. Can you have a health check on a Route 53 Simple Routing policy?
<details>
<summary>Show answer</summary>
<p>
No

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#simple-routing)
</p>
</details>

19. What Route 53 routing would you choose to split traffic 90% to Europe server and 10% to US server?
<details>
<summary>Show answer</summary>
<p>
Weighted Routing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#weighted-routing)
</p>
</details>

20. What Route 53 routing would you choose to route customers to a server based on their Internet connection?
<details>
<summary>Show answer</summary>
<p>
Latency-based Routing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#latency-based-routing)
</p>
</details>

21. What Route 53 routing would you choose to route customers to a different instance or region if a health check fails on the server in the primary instance or region?
<details>
<summary>Show answer</summary>
<p>
Failover Routing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#failover-routing)
</p>
</details>

22. What Route 53 routing would you choose to route United State customers to a US EC2 EC2 instance and European customers to a EU EC2 instance?
<details>
<summary>Show answer</summary>
<p>
Geolocation Routing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#geolocation-routing)
</p>
</details>

23. Does Geolocation Routing take into account latency when deciding which instance or region to direct traffic?
<details>
<summary>Show answer</summary>
<p>
No, only location of the request

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#geolocation-routing)
</p>
</details>

24. To use Geoproximity Routing what must you use in Route 53?
<details>
<summary>Show answer</summary>
<p>
Traffic Flow Only

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#geoproximity-routing-traffic-flow-only)
</p>
</details>

25. What Route 53 routing is basicly the same as Simple Routing but allows you to set up health checks?
<details>
<summary>Show answer</summary>
<p>
Multivalue Answer Routing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#multivalue-answer-routing)
</p>
</details>

26. Think of a VPC as a ____________________.
<details>
<summary>Show answer</summary>
<p>
Logical datacenter in AWS.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

27. What does a VPC consist of?
<details>
<summary>Show answer</summary>
<p>

- Internet Gateways (or Virtual Private Gateways)
- Route Tables
- Network Access COntrol Lists
- Subnets
- Security Groups

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

28. 1 Subnet = ___ Avability Zone?
<details>
<summary>Show answer</summary>
<p>
1

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

29. Security Groups are __________,
<details>
<summary>Show answer</summary>
<p>
Stateful

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

30. Network Access Control Lists are __________,
<details>
<summary>Show answer</summary>
<p>
Stateless

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

31. Can you have Transitive Peering?
<details>
<summary>Show answer</summary>
<p>
No

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

32. When you create a VPC, what is created as default?
<details>
<summary>Show answer</summary>
<p>

- default Route Table
- Network Access Control Lists (NACL)
- default Security Group

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

33. When you create a VPC, what is not created as default?
<details>
<summary>Show answer</summary>
<p>

- any Subnets
- default Internet Gateway

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

34. True or False, `US-East-1A` in your AWS account can be a complettly different availability Zone to `US-East-1A` in another AWS account.
<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

35. Amazon reserves how many IP addresses within your Subnets?
<details>
<summary>Show answer</summary>
<p>
5

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

36. How many Internet Gateways can you have per VPC?
<details>
<summary>Show answer</summary>
<p>
1

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

37. Can Security Groups span VPCs?
<details>
<summary>Show answer</summary>
<p>
No

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#vpc-virtual-private-cloud)
</p>
</details>

38. When creating a NAT instance what should you do to the instance?
<details>
<summary>Show answer</summary>
<p>
Disable Source/Destination Check

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-instances)
</p>
</details>

39. NAT instances must be in what kind of Subnet?
<details>
<summary>Show answer</summary>
<p>
Public

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-instances)
</p>
</details>

40. The ammount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, what should you do?
<details>
<summary>Show answer</summary>
<p>
Increase the instance size

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-instances)
</p>
</details>

41. Are NAT Gateways redundant inside the Availability Zone?
<details>
<summary>Show answer</summary>
<p>
Yes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-gateways)
</p>
</details>

42. Which are prefered for enterprise use, NAT Instance or NAT Gateway?
<details>
<summary>Show answer</summary>
<p>
NAT Gateway

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-gateways)
</p>
</details>

43. Do you need to own the patching maintenance for NAT Gateways?
<details>
<summary>Show answer</summary>
<p>
No

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-gateways)
</p>
</details>

44. Are NAT Gateways automatically assigned a public IP address?
<details>
<summary>Show answer</summary>
<p>
Yes

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-gateways)
</p>
</details>

45. When you create a NAT Gateway what do you need to update so that the NAT Gateway has a route out to the Internet?
<details>
<summary>Show answer</summary>
<p>
Route Tables

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-gateways)
</p>
</details>

46. Do you need to disable Source/Destination Checks with NAT Gateways?
<details>
<summary>Show answer</summary>
<p>
No

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#nat-gateways)
</p>
</details>

47. The default VPC comes with a default Network ACL, how does it handle all inbound and outbound traffic by default?
<details>
<summary>Show answer</summary>
<p>
Allows all outbound and inbound traffic

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

48. When you create a custom Network ACL, how does it handle all inbound and outbound traffic by default?
<details>
<summary>Show answer</summary>
<p>
Denies all outbound and inbound traffic until you add rules

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

49. If you don't associate a Network ACL with each Subet in your VPC what would happen?
<details>
<summary>Show answer</summary>
<p>
The subnet is automatically associated with the default ACL

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

50. What can you use to block IP addresses?
<details>
<summary>Show answer</summary>
<p>
Network ACLs. You cannot block IP addresses with Security Groups

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

51. True or False, you can associate a Network ACL with multiple subnets.
<details>
<summary>Show answer</summary>
<p>
True

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

52. True or False, a subnet can be associated with more than one network ACL at a time.
<details>
<summary>Show answer</summary>
<p>
False

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

53. How are Network ACL rules evaluated?
<details>
<summary>Show answer</summary>
<p>
In numerical order starting with the lowest numbered rule

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#network-access-control-lists)
</p>
</details>

54. A NAT Gateway or NAT Instance is used to provide Internet traffic to EC2 instances in ________________?
<details>
<summary>Show answer</summary>
<p>
a private subnets

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#bastion-host)
</p>
</details>

55. What can you use to securely administer EC2 instances (using SSH or RDP)
<details>
<summary>Show answer</summary>
<p>
Bastion

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#bastion-host)
</p>
</details>

56. True or False, you can use a NAT Gateway as a Bastion Host?
<details>
<summary>Show answer</summary>
<p>
False

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#bastion-host)
</p>
</details>

57. When would you use a AWS Dirrect Connect?
<details>
<summary>Show answer</summary>
<p>

- Useful for high throughput workloads (ie lots of network traffic)
- Useful if you need a stable and reliable secure connection

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#direct-connect)
</p>
</details>

58. What are the kinds of VPC Endpoints?
<details>
<summary>Show answer</summary>
<p>

- Interface Endpoints
- Gateway Endpoints

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#two-types-of-vpc-endpoints)
</p>
</details>

59. What are the services Gateway Endpoints supports?
<details>
<summary>Show answer</summary>
<p>

- S3
- DynamoDB

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#two-types-of-vpc-endpoints)
</p>
</details>
