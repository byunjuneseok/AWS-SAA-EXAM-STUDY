# Section 7. VPCs

## 62. VPC Overview

### What is a VPC?

Think of a VPC as a **virtual data center** in the cloud.

Amazon Virtual Private Cloud (VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

Additionally, you can create a Hardware Virtual Private Network (VPN) connection between your corporate datacenter and your VPC and leverage thr AWS cloud as an extension of your corporate datacenter.

![스크린샷 2019-12-23 오전 10.44.36](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-23 오전 10.44.36.png)

>`10.0.0.0` - `10.255.255.255` : 10/8 prefix
>
>`172.16.0.0` - `172.31.255.255` : 172.16/12 prefix
>
>`192.168.0.0` - `192.168.255.255` : 192.168/16 prefix
>
>🔗 cidr.xyz



### VPC Features

#### What can we do with a VPC?

* Launch instances into a subnet of your choosing
* Assign custom IP address ranges in each subnet
* Configure route tables between subnets
* Create internet gateway and attach it to our VPC
* Much better security control over your AWS resources
* Instance security groups
* Subnet network access control lists (ACLS)



#### Default VPC vs Custom VPC

* Default VPC is user friendly, allowing you to immediately deploy instances.
* All subnets in default VPC have a route out to the internet.
* Each EC2 instance has both a public and private IP address.



#### VPC Peering

* Allows you to connect one VPC with another via a direct network route using private IP addresses.
* Instances behave as if they were on the same private network.
* You can peer VPC's with other AWS account s as well as with other VPCs in the same account.
* Peering is in a star configuration : ie 1 central VPC peers with 4 others. NO TRANSITIVE PEERING!!
* You can peer between regions.

##### No Transitive Peering?

![스크린샷 2019-12-23 오전 10.56.27](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-23 오전 10.56.27.png)

> B -> A -> C 통신을 위해서는 B - C 다이렉트 피어링이 필요하다.



### Exam Tips

* Think of a VPC as a logical datacenter in AWS.
* Constists of IGWs (Or Virtual Private Gateways), Route Tables, Network Access Control List, Subnets, and  security group.
* 1 Subnet = 1 AZ
* **Security Groups are STATEFUL. Network Access Control Lists are STATELESS.**
* NO TRANSITIVE PEERING.



## 63 - 64. Build A Custom VPC

![image-20191223110651134](/Users/byun/Library/Application Support/typora-user-images/image-20191223110651134.png)



#### Reserved IP addresses

* `10.0.0.0` : Network address.
* `10.0.0.1` : Reserved by AWS for the VPC router
* `10.0.0.2` : Reserved by AWS. The IP address of the DNS server is always the base of the VPC network range plust two; however, we also reserve the base of each subnet range plus two. For VPCs with multiple CIDR blocks, the IP address of the DNS server is located in the primary CIDR.
* `10.0.0.3` : Reserved by AWS for future use.
* `10.0.0.255` : Network boradcast address. We do not support broadcast in a VPC, therefore we reserve this address. 

 

![스크린샷 2019-12-23 오전 11.22.08](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-23 오전 11.22.08.png)

&rarr; Create Internet Gateway &rarr; Attach IG to VPC &rarr; Create Route Table (Public / Private) &rarr;

![스크린샷 2019-12-23 오전 10.44.36](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-23 오전 10.44.36.png)



### Exam Tips

* When you create a VPC a default Route Table, Network Access Control List (NACL) and a default Security Group.
* It won't create any subnets, nor will it create a default internet gateway.
* **US-East-1A in your AWS account can be a completely different AZ to US-East-1A in another AWS account. The AZ's are randomized.**
* **Amazon always reserve 5 IP addresses within your subnets.**
* You can on;y have 1 Internet Gateway per VPC.
* Security Groups can't span VPCs.



## 65. Network Address Translation (NAT)

![스크린샷 2019-12-23 오후 12.08.55](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-23 오후 12.08.55.png)

> NAT Instance = Just single EC2 instance
>
> NAT Gateway = High availability Gateway that allows you to get your private subnet, internet, ...


### Exam Tips

#### Nat Instances

* When creating a NAT instance, Disable Source/Destination Check on the Instance.
* NAT instances must be in a public subnet.
* There must be a route out of the private subnet to the NAT instance, in order for this to work.
* The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size.
* You can create high availability using Autoscaling Groups, multiple subnets in different AZs, and a script to automate failover.

* Behind a security group.



#### Nat Gateways

* Redundant inside the AZ
* Preferred by the enterprise.
* Starts at 5Gbps and scales currently to 45Gbps.
* No need to patch
* Not associated with security groups
* Automatically assigned a public IP address
* Remember to update your route tables.
* No need to disable Source/Destination Checks
* If you have resources in multiple AZ and they share one NAT gateway, in the event that the NAT gateway's AZ is down, resources in the other AZ lose internet Access. To create an AZ-independent architecture, create a NAT gateway in each AZ and configure your routing to ensure that resources usethe NAT gateway in the same AZ.



## 66. Network Access Control Lists vs Security Groups

![스크린샷 2019-12-23 오후 12.08.55](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-23 오후 12.08.55.png)

### Exam Tips

* Your VPC automatically comes with a default network ACL, and by default it allows all outbound and inbound traffic.
* You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.
* Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
* Block IP Addresses using network ACLs not security Groups.
* You can associate a network ACL with multiple subnets; however, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
* Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.
* Network ACLs have separate inbound and outbound rules, and each rule can either allow or deny traffic.
* Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic. (and vice versa.)



## 67. Custom VPCs and ELBs

* 최소 두 개 이상의 Subnet이 있어야함.



## 68. VPC FLow logs

VPC Flow logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data is stored using Amazon CloudWatch Logs. After you've created a flow log, you can view and retrieve its data in Aamzon CloudWatch Logs.

#### Flow logs can be created at 3 levels;

* VPC
* Subnet
* Network Interface Level

### Exam TIps

* You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account.
* You cannot tag a flow log.
* After you've created a flow log, you cannot chnage its configuration; for example, you can't associate a different IAM role with the flow log.
*  **Not all IP Traffic is monitored**
  * Traffic generated by instances when they contact the Amazon DNS server. If you use your own DNS server, then all traffic to that DNS server is logged.
  * Traffic generated by a Window instance for Amazon Windows license activation.
  * Traffic to and from 169.254.169.254 for instance metadata.
  * DHCP traffic
  * Traffic to the teserved IP address for the default VPC router.



## 69. Bastions

### Bastion Host

A bastion host is a special purpose computer on a network specifically designed and configured to withstand attacks. The computer generally hosts a single application, for example proxy server, and all other services are removed or limited to reduce the threat to the computer. It is hardened in this manner prilarily due to its location and purpose, which is either on the outside of a firewall or in a demilitarized zone (DMZ) and usually involves access from untrusted networks or computers.

![스크린샷 2019-12-23 오후 3.16.30](img/스크린샷 2019-12-23 오후 3.16.30.png)



![스크린샷 2019-12-23 오후 3.17.27](img/스크린샷 2019-12-23 오후 3.17.27.png)

> Private SN 에 있는 인스턴스는 인터넷을 접속할 일이 생긴다. (패치, 설치 등의 목적...)



![스크린샷 2019-12-23 오후 3.19.13](img/스크린샷 2019-12-23 오후 3.19.13.png)

> 밖에서 SSH or RDP 접속을한다면... Bastion 이 포워드해줌.



### Exam Tips 

* A NAT gateway or NAT instance is used to provide internet traffic to EC2 instances in a private subnets.
* A Bastion is used to securely administer EC2 instances (Using SSH or RDP). Bastions are called *Jump Boxes* in Australia.
* You cannot use a NAT Gateway as a Bastion host.



## 70. Direct Connect

AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated mnetwork connection from your premises to AWS. Using AWS Direct Connect, you can establish private connectivity between AWS and your datacenter, office, or colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet-based connection.

![스크린샷 2019-12-23 오후 3.28.11](img/스크린샷 2019-12-23 오후 3.28.11.png)



### Exam Tips

* Driect Connect directly connects your data center to AWS.
* Useful for high throughput workloads (ie lost of network traffic)
* Or if you need a stable and reliable secure connection.





## 71. VPC End Points

A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection. or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon Network.

Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.



### Two Types of VPC endpoints:

* Interface Endpoints
* Gateway Endpoints

#### Interface Endpoints support

![스크린샷 2019-12-23 오후 3.32.50](img/스크린샷 2019-12-23 오후 3.32.50.png)

#### Currently Gateway Endpoints support

* Amazon s3
* DynamoDB



### VPC EndPoints In Action

![스크린샷 2019-12-23 오후 3.34.53](img/스크린샷 2019-12-23 오후 3.34.53.png)

CHANGE THIS ARCHITECTURE LIKE BELOW! 

![스크린샷 2019-12-23 오후 3.36.19](img/스크린샷 2019-12-23 오후 3.36.19.png)