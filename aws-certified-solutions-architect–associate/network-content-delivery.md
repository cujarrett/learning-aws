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

## Elastic Load Balancer (ELB)
Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. Elastic Load Balancing offers three types of load balancers that all feature the high availability, automatic scaling, and robust security necessary to make your applications fault tolerant.

- ELBs are given their own DNS name. You are never given an IP address for an ELB.
- [ELB FAQ](https://aws.amazon.com/elasticloadbalancing/faqs/)

### ELB Status
ELB Status is either reported as `InService` or `OutOfService`.

### Health Checks
Health Checks check the instance health by talking to it.

### ELB Types
- #### Application Load Balancer
    Application Load Balancerare best suited for load balancing of HTTP and HTTPS traffic. They opperate at Layer 7 and are application aware. They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers.

- #### Network Load Balancer
    Network Load Balancer are best suited for load balancing of TCP traffic where extream performance is required. Operating at the connection level (Layer 4), Network Load Balancer are capable of handling millions of requests per second, while maintaining ultra-low latencies. Use for extream performance.

- #### Classic Load Balancer
    Classic Load Balancer are legacy Elastic Load Balancers. You can load balance HTTP/HTTPS applications and use Layer 7 specific features such as X-Forwarded and sticky sessions. You can also use strict Layer 4 load balancing for applications that rely purely on the TCP protocol.

### ELB Errors
If your application stops responding, the ELB (Classic Load Balancer) responds with a 504 (GateWay Timeout) error. This means that the application is having issues. This could be either at the Web Server layer or at the Database layer. Identy where the application is failing, and scale it up or out where possible.

### X-Forwarded-For Header
Holds the users IPv4 address, useful when a user goes through a load balancer before hitting your app.

### Advanced Load Balancer Theory
- ### Sticky Sessions
    Classic Load Balancer routes each request independently to the registered EC2 instance with the smallest load. Sticky Sessions allow you to bind a user's session to a specific EC2 instance. This ensures that all requests from the user during the session are sent to the same instance.

    You can enable Sticky Sessions for Application Load Balancers as well, but the traffic will be sent at the Target Group Level.

    If you have EC2 instances that are receiving no traffic you can disable Sticky Sessions to fix that problem.

- ### Cross Zone
    With cross-zone load balancing, each load balancer node for your Classic Load Balancer distributes requests evenly across the registered instances in all enabled Availability Zones. If cross-zone load balancing is disabled, each load balancer node distributes requests evenly across the registered instances in its Availability Zone only.
- ### Path Patterns
    You can create a listenerwith rules to forward requests based on the URL path. This is known as path-based routing. If you are running microservices, you can route traffic to multiple back-end services using path-based routing. For example, you can route general requests to one target group and requests to render images to another target group.

## HA Architecture
![HA Architecture example](https://user-images.githubusercontent.com/16245634/71314232-15121180-240a-11ea-8421-397e7bdc5961.png)
Everything fails. Everything. You should plan for failure.

- Design for failure
- Use multiple Availability Zones and multiple Regions where ever you can
- Know the difference between Multi Availability Zone and Read Replicas for RDS
- Know the difference between scaling out and scaling up
  - Scaling out could be autoscaling EC2 instances
  - Scaling up could be increasing the resources in each EC2 instance, aka going from a T2 micro to a 6X instance
- Know the different S3 storage classes, standard S3 is high availability by default, reduced redundancy and S3 single Availability Zone are not highly available

## API Gateway
API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale.

With a few clicks in the AWS Management Console, you can create an API that acts as a "front door" for applications to access datam business logic, or functionality from your back end services, such as applications runnon on EC2, code running in Amazon Lambda, or any web application.

- API Gateway has caching capabilities to increase performance
- API Gateway is low cost and scales automatically
- You can throttle API Gateway to prevent attacks
- You can log results to CloudWatch
- If you are using JavaScript/AJAX that uses multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway
- CORS is enforced by the client

### What can an API Gateway do?
- Expose HTTPS endpoints to define a RESTful API
- Serverless-ly connect to services like Lambda & DynamoDB
- Send each API endpoint to a different target
- Run efficently with low cost
- Scale effortlessly
- Track and control usage by API key
- Throttle requests to prevent attacks
- Connect to CloudWatch to log all requests for monitoring
- Maintain multiple versions of your API

### How do I configure an API Gateway?
- Define an API (container)
- Define Resources and nested Resources (URL paths)
- For each Resource:
  - Select supported HTTP methods (verbs)
  - Set security
  - Choose target (such as EC2, Lambda, DynamoDB, etc)
  - Set request and response transformations

### How do I deploy an API Gateway?
- Deploy API to a stage
  - Uses API Gateway domain by default
  - Can use custom domain
  - Now supports AWS Certificate Manager: free SSL/TLS certs

### API Gateway Caching
You can enable API Caching in Amazon API Gateway to cache your endpoints response. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of the requests to your API. When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time to live (TTL) period in seconds. API Gateway then responds to the request by looking up the endpoint response from the cache instead of making a request to your endpoint.

### Same Origin Policy
In computing, the same origin policy is an important concept in the web application security model. Under the policy, a web browser permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin.

This is done to prevent Cross Site Scripting (XSS) attacks.

- Enforced by browsers but some tools like PostMan and curl ignore it

### CORS
CORS is one way the server at the other end (not the client clode in the browser) can relax the same origin policy.

Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources (eg fonts) on a web page to be requested from another domain outside the domain from which the first resource was served.

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

60. VPC stands for:
- a. Very Private Cloud
- b. Virtual Public Cloud
- c. Virtual Private Cloud
- d. Very Public Cloud

<details>
<summary>Show answer</summary>
<p>
- c. Virtual Private Cloud
</p>
</details>

61. Having just created a new VPC and launching an instance into its public subnet, you realise that you have forgotten to assign a public IP to the instance during creation. What is the simplest way to make your instance reachable from the outside world?
- a. Create an Elastic IP and new network interface. Associate the Elastic IP to the new network interface, and the new network interface to your instance.
- b. Associate the private IP of your instance to the public IP of the internet gateway.
- c. Create an Elastic IP address and associate it with your instance.
- d. Nothing – by default all instances deployed into any public subnet will automatically receive a public IP.

<details>
<summary>Show answer</summary>
<p>
- c. Create an Elastic IP address and associate it with your instance.

Although creating a new NIC & associating an EIP also results in your instance being accessible from the internet, it leaves your instance with 2 NICs & 2 private IPs as well as the public address and is therefore not the simplest solution. By default, any user-created VPC subnet WILL NOT automatically assign public IPv4 addresses to instances – the only subnet that does this is the “default” VPC subnets automatically created by AWS in your account.
</p>
</details>

62. True or False: A subnet can span multiple Availability Zones.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False

Each subnet must reside entirely within one Availability Zone and cannot span zones.
</p>
</details>

63. Are you permitted to conduct your own vulnerability scans on your own VPC without alerting AWS first?
- a. Yes. You can perform any scan without alerting AWS first.
- b. No. You must always alert AWS before performing any type of vulnerability scan
- c. Depends on the type of scan and the service being scanned. Some scans can be performed without alerting AWS, some require you to alert.

<details>
<summary>Show answer</summary>
<p>
- c. Depends on the type of scan and the service being scanned. Some scans can be performed without alerting AWS, some require you to alert.

Until recently customers were not permitted to conduct penetration testing without AWS engagement. However that has changed. There are still conditions though.
</p>
</details>

64. By default, instances in new subnets in a custom VPC can communicate with each other across Availability Zones.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False

In a custom VPC with new subnets in each AZ, there is a route that supports communication across all subnets/AZs. Plus a default SG with an allow rule 'All traffic, all protocols, all ports, from anything using this default SG'.
</p>
</details>

65. True or False: You can accelerate your application by adding a second internet gateway to your VPC.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False

You may have only one internet gateway per VPC.
</p>
</details>

66. When peering VPCs, you may peer your VPC only with another VPC in your same AWS account.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- b. False

You may peer a VPC to another VPC that's in your same account, or to any VPC in any other account.
</p>
</details>

67. True or False: An application load balancer must be deployed into at least two subnets.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True

An application load balancer must be deployed into at least two subnets.
</p>
</details>

68. Which of the following is a chief advantage of using VPC endpoints to connect your VPC to services such as S3?
- a. Traffic between your VPC and the other service does not leave the Amazon network.
- b. VPC Endpoints offer a faster path through the public internet than you can realize with a NAT instance.
- c. VPC Endpoints require public IP addresses, offering rapid connectivity from the public internet.
- d. VPC endpoints are dedicated hardware devices that cannot be accessed without the correct IAM credentials.

<details>
<summary>Show answer</summary>
<p>
- a. Traffic between your VPC and the other service does not leave the Amazon network.

In contrast to a NAT gateway, traffic between your VPC and the other service does not leave the Amazon network when using VPC endpoints.
</p>
</details>

69. Which of the following allows you to SSH or RDP into an EC2 instance located in a private subnet?
- a. Bastion Hosts
- b. NAT Instance
- c. NAT Gateway
- d. Internet Gateway

<details>
<summary>Show answer</summary>
<p>
- a. Bastion Hosts

A Bastion host allows you to securely administer (via SSH or RDP) an EC2 instance located in a private subnet. Don't confuse Bastions and NATs, which allow outside traffic to reach an instance in a private subnet.
</p>
</details>

70. How many internet gateways can I attach to my custom VPC 
- a. 1
- b. 2
- c. 3
- d. One per Availability Zone

<details>
<summary>Show answer</summary>
<p>
- a. 1
</p>
</details>

71. You have five VPCs in a 'hub and spoke' configuration, with VPC 'A' in the center and individually paired with VPCs 'B', 'C', 'D', and 'E', which make up the 'spokes'. There are no other VPC connections. Which of the following VPCs can VPC 'B' communicate with directly?
- a. VPC A
- b. VPC A and VPC C
- c. VPC A and VPC E
- d. VPC C, VPC D, and VPC E

<details>
<summary>Show answer</summary>
<p>
- a. VPC A

As transitive peering is not allowed, VPC 'B' can communicate directly only with VPC 'A'.
</p>
</details>

72. Which of the following is true?
- a. Security Groups are stateful and Network Access Control Lists are stateless
- b. Security Groups are stateless and Network Access Control Lists are stateful
- c. Both Security Groups and Network Access Control Lists are stateless
- d. Both Security Groups and Network Access Control Lists are stateful 

<details>
<summary>Show answer</summary>
<p>
- a. Security Groups are stateful and Network Access Control Lists are stateless

Security Groups are stateful and Network Access Control Lists are stateless.
</p>
</details>

73. Which of the following offers the largest range of internal IP addresses?
- a. /16
- b. /28
- c. /24
- d. /20

<details>
<summary>Show answer</summary>
<p>
- a. /16

The /16 offers 65,536 possible addresses.
</p>
</details>

74. Security groups act like a firewall at the instance level, whereas _________ are an additional layer of security that act at the subnet level.
- a. Network ACLs
- b. DB Security Groups
- c. VPC Security Groups
- d. Route Tables

<details>
<summary>Show answer</summary>
<p>
- a. Network ACLs
</p>
</details>

75. In a default VPC, all Amazon EC2 instances are assigned two IP addresses at launch. What are they?
- a. A private IP address and a public IP address
- b. A public IP address and a secret IP address
- c. An elastic IP address and a public IP address
- d. An IPv6 address and an Elastic IP address

<details>
<summary>Show answer</summary>
<p>
- a. A private IP address and a public IP address
</p>
</details>

76. When I create a new security group, all outbound traffic is allowed by default.
- a. True
- b. False

<details>
<summary>Show answer</summary>
<p>
- a. True
</p>
</details>

77. By default, how many VPCs am I allowed in each AWS region?
- a. 1
- b. 2
- c. 6
- d. 5

<details>
<summary>Show answer</summary>
<p>
- d. 5
</p>
</details>

78. Select the incorrect statement.
- a. In Amazon VPC, an instance retains its private IP
- b. It is possible to have private subnets in a VPC
- c. In Amazon VPC, an instance does not retain its private IP
- d. You may have only 1 Internet Gateway per VPC

<details>
<summary>Show answer</summary>
<p>
- c. In Amazon VPC, an instance does not retain its private IP
</p>
</details>

79. To save administration headaches, a consultant advises that you leave all security groups in web-facing subnets open on port 22 to 0.0.0.0/0 CIDR. That way, you can connect wherever you are in the world. Is this a good security design?
- a. Yes
- b. No

<details>
<summary>Show answer</summary>
<p>
- b. No

0.0.0.0/0 would allow ANYONE from ANYWHERE to connect to your instances. This is generally a bad plan. The phrase 'web-facing subnets' does not mean just web servers. It would include any instances in that subnet some of which you may not strangers attacking. You would only allow 0.0.0.0/0 on port 80 or 443 to to connect to your public facing Web Servers, or preferably only to an ELB. Good security starts by limiting public access to only what the customer needs. Please see the AWS Security whitepaper for complete details.
</p>
</details>

80. What are the three kinds of load balancers?
<details>
<summary>Show answer</summary>
<p>

- Classic Load Balancer
- Application Load Balancer
- Network Load Balancer

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#elb-types)
</p>
</details>

81. What does a 504 Error mean?
<details>
<summary>Show answer</summary>
<p>
The gateway has timed out. The application is not responding within the idle timeout period.

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#elb-errors)
</p>
</details>

82. What should you do when you see a 504 Error?
<details>
<summary>Show answer</summary>
<p>
Troubleshoot the application. Is it the Web Server or the Database Server?

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#elb-errors)
</p>
</details>

83. If you are using a Load Balancer and need the IP address of your end user what can you use to accomplish this?
<details>
<summary>Show answer</summary>
<p>
X-Forwarded-For

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#x-forwarded-for-header)
</p>
</details>

83. What are the status reported for instances monitored by ELB?
<details>
<summary>Show answer</summary>
<p>

- InService
- OutOfService

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#elb-status)
</p>
</details>

84. How can you check the instance health?
<details>
<summary>Show answer</summary>
<p>
Health Checks talk to the instance

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#health-checks)
</p>
</details>

85. How do you access a Load Balancer?
<details>
<summary>Show answer</summary>
<p>
DNS Name, you are never given an IP address for a Load Balancer

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#elastic-load-balancer-elb)
</p>
</details>

86. How can you ensure users of your load balanced application stay in the same instance for the duration of their interactions?
<details>
<summary>Show answer</summary>
<p>
Sticky Sessions

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#sticky-sessions)
</p>
</details>

87. How can you load balance across multiple availability zones?
<details>
<summary>Show answer</summary>
<p>
Cross Zone Load Balancing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#cross-zone)
</p>
</details>

88. How can you load balance your application to different EC2 instances based on the URL contained in the request?
<details>
<summary>Show answer</summary>
<p>
Path Patterns Load Balancing

[More info](https://github.com/cujarrett/learning-aws/blob/master/aws-certified-solutions-architect%E2%80%93associate/network-content-delivery.md#path-patterns)
</p>
</details>

89. You have a website with three distinct services, each hosted by different web server autoscaling groups. Which AWS service should you use?
- a. S3 Static websites
- b. Elastic Load Balancers (ELB)
- c. Application Load Balancers (ALB)
- d. Classic Load Balancers (CLB)
- e. Network Load Balancers (NLB)

<details>
<summary>Show answer</summary>
<p>
- c. Application Load Balancers (ALB)

The ALB has functionality to distinguish traffic for different targets (mysite.co/accounts vs. mysite.co/sales vs. mysite.co/support) and distribute traffic based on rules for target group, condition, and priority.
</p>
</details>

90. You manage a high-performance site that collects scientific data using a bespoke protocol over TCP port 1414. The data comes in at high speed and is distributed to an autoscaling group of EC2 compute services spread over three AZs. Which type of AWS load balancer would best meet this requirement?
- a. CloudFront combined with Lambda@Edge
- b. Elastic Load Balancers (ELB)
- c. Application Load Balancers (ALB)
- d. Network Load Balancers (NLB)

<details>
<summary>Show answer</summary>
<p>
- d. Network Load Balancers (NLB)

The Network Load Balancer is specifically designed for high performance traffic that is not conventional web traffic. The Classic LB might also do the job, but would not offer the same performance.
</p>
</details>

91. You have been tasked with creating a resilient website for your company. You create the Classic Load Balancer with a standard health check, a Route 53 alias pointing at the ELB, and a launch configuration based on a reliable Linux AMI. You have also checked all the security groups, NACLs, routes, gateways and NATs. You run the first test and cannot reach your web servers via the ELB or directly. What might be wrong?
- a. The launch configuration is not being triggered correctly
- b. The health check is not set up correctly
- c. Your autoscaling group is set to zero instances
- d. You have specified the wrong key pair and the servers cannot start the http service properly

<details>
<summary>Show answer</summary>
<p>
- a. The launch configuration is not being triggered correctly

In a question like this you need to evaluate if all the necessary services are in place. The glaring omission is that you have not built an autoscaling group to invoke the launch configuration you specified. The instance count and health check depend on instances being created by the autoscaling group. Finally, key pairs have no relevance to services running on the instance.
</p>
</details>

92. If you are told that an EC2 instance is being changed to have more RAM, Is this considered scaling up or scaling out?
- a. Scaling out
- b. Scaling up

<details>
<summary>Show answer</summary>
<p>
- b. Scaling up

Scaling out is where you have more of the same resource separately working in parallel (visualize services sitting side by side). Scaling up is where you make it bigger and bigger like and ugly tower with more floors being added after the initial design was finished.
</p>
</details>

93. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that you can access a resource or service when you need it?
- a. Availability
- b. Durability
- c. Resilency
- d. Reliability

<details>
<summary>Show answer</summary>
<p>
- a. Availability

Each word has a specific meaning and your ability to select the correct answer may depend on understanding the difference. Availability can be described as the % of a time period when the service will be able to respond to your request in some fashion.
</p>
</details>

94. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that a resource will continue to exist until you decide to remove it?
- a. Availability
- b. Durability
- c. Resilency
- d. Reliability

<details>
<summary>Show answer</summary>
<p>
- b. Durability

Each word has a specific meaning and your ability to select a correct answer may depend on understanding the difference. Durability refers to the on-going existence of the object or resource. Note that it does not mean you can access it, only that it continues to exist.
</p>
</details>

95. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that a resource ability to recover from damage or disruption?
- a. Availability
- b. Durability
- c. Resilency
- d. Reliability

<details>
<summary>Show answer</summary>
<p>
- c. Resilency

Each word has a specific meaning and your ability to select the correct answer may depend on understanding the difference. Resiliency can be described as the ability to a system to self heal after damage or an event. Note that this does not mean that it will be available continuously during the event, only that it will self recover.
</p>
</details>

96. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that a resource will work as designed?
- a. Availability
- b. Durability
- c. Resilency
- d. Reliability

<details>
<summary>Show answer</summary>
<p>
- d. Reliability

Each word has a specific meaning and your ability to select a correct answer may depend on understanding the difference. Reliability is closely related to availability, however a system can be 'available' but not be working properly. Reliability is the probability that a system will work as designed. This term is not used much in AWS, but is still worth understanding.
</p>
</details>

97. You work for a major news network in Europe. They have just released a new mobile app that allows users to post their photos of newsworthy events in real-time. Your organization expects this app to grow very quickly, essentially doubling its user base each month. The app uses S3 to store the images, and you are expecting sudden and sizable increases in traffic to S3 when a major news event takes place (as users will be uploading large amounts of content.) You need to keep your storage costs to a minimum, and you are happy to temporally lose access to up to 0.1% of uploads per year. With these factors in mind, which storage media should you use to keep costs as low as possible?
- a. S3 Standard IA
- b. S3 Standard
- c. S3 One Zone Infrequent Access
- d. S3 Reduced Redundancy Storage (RRS)
- e. Glacier
- f. S3 Provisioned IOPS

<details>
<summary>Show answer</summary>
<p>
- a. S3 Standard IA

The key drivers here are availability and cost, so an awareness of cost is necessary to answer this. Full S3 is quite expensive at around $0.023 per GB for the lowest band. S3 standard IA is $0.0125 per GB, S3 OneZone-IA is $0.01 per GB, and Legacy S3-RRS is around $0.024 per GB for the lowest band. Of the offered solutions S3 One Zone-IA is the cheapest suitable option. Glacier cannot be considered as it is not intended for direct access, however it comes in at around $0.004 per GB. S3 has an availability of 99.99%, S3-IA has an availability of 99.9% while S3-1Zone-IA only has 99.5%.
</p>
</details>

98. You work for a manufacturing company that operate a hybrid infrastructure with systems located both in a local data center and in AWS, connected via AWS Direct Connect. Currently, all on-premise servers are backed up to a local NAS, but your CTO wants you to decide on the best way to store copies of these backups in AWS. He has asked you to propose a solution which will provide access to the files within milliseconds should they be needed, but at the same time minimizes cost. As these files will be copies of backups stored on-premise, availability is not as critical as durability. Choose the best option from the following which meets the brief.
- a. Copy the files form the NAS to an S3 bucket configured as Standard class
- b. Copy the files to an EC2 instance with a large EBS volume attached
- c. Copy the files from the NAS to an S3 bucket with the One Zone IA class
- d. Copy the files from the NAS to an S3 bucket with the Reduced Redundancy Storage class

<details>
<summary>Show answer</summary>
<p>
- c. Copy the files from the NAS to an S3 bucket with the One Zone IA class

S3 OneZone-IA provides on-line access to files, while offering the same 11 9's of durability as all other storage classes. The trade-off is in the availability - 99.5% as opposed to 99.9%-99.99%. However in this brief as cost is more important than availability, S3 OneZone-IA is the logical choice . RRS is deprecated and new uses are strongly discouraged by AWS.
</p>
</details>

99. You need to use an object-based storage solution to store your critical, non-replaceable data in a cost-effective way. This data will be frequently updated and will need some form of version control enabled on it. Which S3 storage solution should you use?
- a. S3
- b. S3 IA
- c. S3 One Zone IA
- d. S3 RRS
- e. Glacier

<details>
<summary>Show answer</summary>
<p>
- a. S3

The key point in the questions is that the data is non-replaceable and is frequently updated. The 1st excludes anything the has reduced durability, the second excluded anything with long recall, reduced availability, or billing based on infrequent access.
</p>
</details>

100. In S3 the durability of my files is ________.
- a. 99.99%
- b. 99.999999999%
- c. 99%
- d. 100%

<details>
<summary>Show answer</summary>
<p>
- b. 99.999999999%
</p>
</details>

101. When you have deployed an RDS database into multiple availability zones, can you use the secondary database as an independent read node?
- a. No
- b. Only in US-West-1
- c. It depends on how you set it up
- d. Yes

<details>
<summary>Show answer</summary>
<p>
- a. No
</p>
</details>

102. Placement groups can either be of the type 'cluster', 'spread', or 'partition'. Choose options from below which are only specific to Spread Placement Groups.
- a. Spread placement groups require a name that is unique within your AWS account for the region
- b. An instance can be launched in one placement group at a time and cannot span multiple placement groups
- c. A spread placement group is a logical grouping of instances within a single Availability Zone
- d. A spread placement group is a group of instances that are each placed on distinct underlying hardware

<details>
<summary>Show answer</summary>
<p>
- d. A spread placement group is a group of instances that are each placed on distinct underlying hardware

There is only one answer that is specific to Spread Placement Groups, and that is the final option. Whilst some of these answers are correct for either Cluster Placement Groups only, or for both Cluster and Spread Placement Groups, the question stated that only options specific to Spread Placement Groups should be chosen. This would rule out two options as they are true for both Spread & Cluster type placement groups. The Logical grouping of instances within a single Availability Zone is only true of Cluster Placement Groups and is also incorrect.
</p>
</details>

103. Can I "force" a failover for any RDS instance that has multi-AZ configured?
- a. Yes
- b. No
- c. Only for Oracle RDS instances

<details>
<summary>Show answer</summary>
<p>
- a. Yes
</p>
</details>
