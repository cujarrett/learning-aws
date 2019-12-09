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

- #### Weighted Routing
  ![Weighted Routing example](https://user-images.githubusercontent.com/16245634/70397476-2e619980-19d8-11ea-8291-f99f8a820976.png)
  Allows you to split your traffic based on different weights assigned. For example, you can set 10% of your traffic to go to `US-EAST-1` and 90% to go to `EU-WEST-1`.

- #### Latency-based Routing
  ![Latency-based Routing example](https://user-images.githubusercontent.com/16245634/70398028-d2e5da80-19dc-11ea-941f-c48c65efb696.png)
  Latency-based Routing allows you to route your traffic based on the lowest network latency for your end user (ie which region will give them the fastest response time).
  
  To use Latency-based Routing, you create a latency resource record set for the Amazon EC2 (or ELB) resource in each region that hosts your website. When AmazonRoute 53 receives a query for your site, it selects the latency resource record set for the region that gives the lowest latency. Route 53 then responds with the value associated with that resource record set.

- ##### Failover Routing
  ![Failover Routing example](https://user-images.githubusercontent.com/16245634/70398195-8a2f2100-19de-11ea-9db7-3c839296ee59.png)
  Failover Routing policies are used when you want to create an activity/ passive set up. For example, you may want your primary site in `EU-WEST-2` and your secondary DR site in `AP-SOUTHEAST-2`.

  Route 53 will monitor the health of your primary site using a health check.

  A health check monitors the health of your end points.

- ##### Geolocation Routing
  ![Geolocational Routing example](https://user-images.githubusercontent.com/16245634/70398395-88fef380-19e0-11ea-86ff-f069ce9678ab.png)
  Geolocation Routing lets you choose where your traffic will be sent based on the geographic location of your users (ie the location from which DNS queries originate). For example, you may want all queries from Europe to be routed to a fleet of EC2 instanes that are specifically configured for your European customers. These servers may have the local language of your European customers and all prices are displayed in Euros.

- ##### Geoproximity Routing (Traffic Flow Only)
  Geoproximity Routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and  your resources. You can also optionally choose to route more traffic or less traffic to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

  To use Geoproximity Routing, you must use Route 53 Traffic Flow

- ##### Multivalue Answer Routing
  Multivalue Answer Routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record, but Multivalue Answer Routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources.
  
  **This is similar to Simple Routing however it allows you to put health checks on each record set.**

### Route 53 Health Checks
- You can set health checks on individual recordds sets
- If a record set fails a health check it will be removed from Route53 until it passes the health 
- You can set SNS notifications to alert you if a health check is failed
