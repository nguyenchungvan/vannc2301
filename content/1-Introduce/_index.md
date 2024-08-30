---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
**Amazon Elastic Compute Cloud (EC2)** is a cloud computing service from AWS that provides scalable and flexible computing power. EC2 allows you to launch virtual servers (also known as instances) to run applications in the AWS cloud environment.

**Amazon Virtual Private Cloud (VPC)** is a service provided by Amazon Web Services (AWS) that allows users to create a private virtual network within the AWS cloud environment. With VPC, you can configure your own virtual network, including dividing it into subnets, setting up route tables, and managing gateways, all within a separate and secure space.

Key Features of Amazon VPC:

- Private Networking: Create a virtual network with private IPs and configure private IPs for resources within the VPC.
- Network Segmentation: Divide the VPC into public and private subnets to categorize and control traffic flow.
- Gateways and Routing: Use Internet Gateway, NAT Gateway, and Route Tables to control access to and from the VPC.
- Security: Manage traffic with Security Groups and Network ACLs, and use VPC Peering to connect with other VPCs or on-premises networks.
  
**Subnet** is a range of IP addresses within your VPC. Subnets are used to divide a large network into smaller, more manageable sections and can optimize performance and security. Additionally, subnets are created to connect to AWS resources such as EC2 and RDS when you launch them. Subnets can connect to the internet, other VPCs, or your data center and route traffic through route tables.

**Route table** is a data structure in a network system used to determine how data traffic is routed to its destination within the network. Each route in the table specifies the IP address range where you want the traffic to go (destination) and the intermediate point (gateway, network interface, or connection) through which the traffic will pass before reaching the target (destination).
Internet Gateway (IGW) is a networking service in Amazon Web Services (AWS) that connects your resources in a VPC (Virtual Private Cloud) to the Internet. It acts as a connection point between the VPC and the Internet, allowing resources within the VPC to send and receive traffic from the Internet.

**NAT (Network Address Translation) Gateway** is an AWS service that provides internet access to resources within a VPC without allowing direct traffic from the Internet to those resources. NAT Gateway enables instances in a private subnet to send traffic to the Internet and receive responses without needing a Public IP.

**Public IP** is an IP address that a device or service uses to communicate directly with the Internet or other devices outside the local network. This address must be unique across the entire Internet. **Private IP** is an IP address used within a local network and cannot be accessed directly from the Internet. Private IPs are used for communication between devices within the same local network.

**Security Group** is an essential feature of Amazon Web Services (AWS) that helps manage and control inbound and outbound network traffic for resources such as EC2 instances, RDS instances, and other services within a VPC (Virtual Private Cloud). Security Groups have two main features:

- Stateful Firewall: If you allow an inbound connection, responses from that connection are automatically allowed back, regardless of outbound rules, and vice versa.
- Connection Tracking: Security Groups maintain information about current network connections. This means that once a connection is established and allowed by an inbound rule, all responses from that connection are also allowed, even if there is no corresponding outbound rule.

**Network Access Control List (NACL)** is a security mechanism in AWS used to control incoming and outgoing traffic for subnets within a Virtual Private Cloud (VPC). NACL operates at the subnet level and provides an additional layer of security beyond Security Groups, helping manage and control access to resources within the VPC. NACL characteristics:

- Stateless: Each request in or out is evaluated independently according to the NACL rules. If you allow inbound traffic, you must also create a rule to allow outbound traffic.
- Unlike Security Groups, NACL rules can be set to explicitly allow or deny specific traffic.

An example of using NACL is when you need to block an IP address that has been connecting to an instance. While you can remove the user's inbound rules in the Security Group, the connection between the user and the instance continues due to the connection tracking feature of the Security Group. With NACL, adding a rule to deny connections from the user's IP will immediately disconnect the user from the instance.

**Amazon Relational Database Service (RDS)** is a fully managed relational database service by AWS. It simplifies the management of relational databases in the cloud environment, offering flexible scalability, robust security, and high availability, enabling you to focus on developing applications without worrying about complex database management.

