# AWS Global Infrastructure

## Availability Zones
A Data Center is a building in the country side or in the city that's filled with computer tech like servers, SANS, switches, firewalls, load balancers, storage. An Availability Zone could be one data center or several close together of data centers within a couple of miles of each other.

## Regions
A Region is a physical location, a geographical area consistenting of two or more Availability Zones.

## Edge Locations
Edge Locations are endpoints for AWS which are used for caching content. Typically consists of CloudFront (Amazon's Content Delivery Network (CDN)). There are many more Edge Locations than Regions. There are more than 150 Edge Locations as of 2019.

## AWS Global Infrastructure Review
1. What does VPC stand for?
- a. Virtual Public Compute
- b. Virtual Private Cloud
- c. Virtual Public Cloud
- d. Virtual Private Compute

<details>
<summary>Show answer</summary>
<p>
- b. Virtual Private Cloud
</p>
</details>

2. An AWS VPC is a compute of which group of AWS services?
- a. Global Infrastructure
- b. Database Services
- c. Networking Services
- d. Compute Services

<details>
<summary>Show answer</summary>
<p>
- c. Networking Services

A Virtual Private Cloud (VPC) is a virtual network dedicated to a single AWS account. It is logically isolated from other virtual networks in the AWS cloud, providing compute resources with security and robust networking functionality.
</p>
</details>

3. What Does an AWS Region consist of?
- a. A console that gives you a quick, global picture of your cloud computing environment.
- b. A collection of databases that can only be accessed from a specific geographic region.
- c. A collection of data centers that is spread evenly around a specific continent.
- d. A distinct location within a geographic area designed to provide high level availability to a specific geography.

<details>
<summary>Show answer</summary>
<p>
- d. A distinct location within a geographic area designed to provide high level availability to a specific geography.

Each region is a separate geographic area. Each region has multiple, isolated locations known as Availability Zones.
</p>
</details>

4. Which statement best describe Availability Zones?
- a. A content Distribution Network used to distribute content to users.
- b. Restricted areas designed specifically for the creation of Virtual Private Clouds.
- c. Two zones containing compute resources that are designed to automatically maintain synchronized copies of each other's data.
- d. Distinct locations from within an AWS region that are engineered to be isolated from failures.

<details>
<summary>Show answer</summary>
<p>
- d. Distinct locations from within an AWS region that are engineered to be isolated from failures.

An Availability Zone (AZ) is a distinct location within an AWS Region. Each Region comprises at least two AZs.
</p>
</details>

5. What is an AWS region?
- a. A region is an independent data center, located in different countries around the globe.
- b. A region is a geographic area divided into Availability Zones. Each region contains at least two Availability Zones.
- c. A region is a collection of Edge Locations available in specific countries.
- d. A region is a subset of AWS technologies. For example, the Compute region consists of EC2, ECS, Lambda, etc.

<details>
<summary>Show answer</summary>
<p>
- b. A region is a geographic area divided into Availability Zones. Each region contains at least two Availability Zones.

A region is a geographical area divided into Availability Zones. Each region contains at least two Availability Zones.
</p>
</details>

6. Which of the following is correct?
- a. # Regions > # Availability Zones > # of Edge Locations
- b.  # Availability Zones  > # Regions > # of Edge Locations
- c. # of Edge Locations > # Availability Zones > # Regions
- d.  # Availability Zones >  # of Edge Locations > # Regions

<details>
<summary>Show answer</summary>
<p>
- c. # of Edge Locations > # Availability Zones > # Regions

The number of Edge Locations is greater than the number of Availability Zones, which is greater than the number of Regions.
</p>
</details>

7. In which of the following is CloudFront content cached?
- a. Availability Zones
- b. Region
- c. Edge Location
- d. Data Center

<details>
<summary>Show answer</summary>
<p>
- c. Edge Location

CloudFront content is cached in Edge Locations.
</p>
</details>
