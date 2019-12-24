# Quiz

1. VPC stands for:

- Very Private Cloud
- Virtual Public Cloud
- **Virtual Private Cloud**
- Very Public Cloud



2. Having just created a new VPC and launching an instance into its public subnet, you realise that you have forgotten to assign a public IP to the instance during creation. What is the simplest way to make your instance reachable from the outside world?

- Create an Elastic IP and new network interface. Associate the Elastic IP to the new network interface, and the new network interface to your instance.
- Associate the private IP of your instance to the public IP of the internet gateway.
- **Create an Elastic IP address and associate it with your instance.**
- Nothing – by default all instances deployed into any public subnet will automatically receive a public IP.

> Although creating a new NIC & associating an EIP also results in your instance being accessible from the internet, it leaves your instance with 2 NICs & 2 private IPs as well as the public address and is therefore not the simplest solution. By default, any user-created VPC subnet WILL NOT automatically assign public IPv4 addresses to instances – the only subnet that does this is the “default” VPC subnets automatically created by AWS in your account.



3. True or False: A subnet can span multiple Availability Zones.

- **FALSE**
- TRUE



4. Are you permitted to conduct your own vulnerability scans on your own VPC without alerting AWS first?

- Yes. You can perform any scan without alerting AWS first.
- No. You must always alert AWS before performing any type of vulnerability scan
- **Depends on the type of scan and the service being scanned. Some scans can be performed without alerting AWS, some require you to alert.**

> Until recently customers were not permitted to conduct penetration testing without AWS engagement. However that has changed. There are still conditions though.



5. By default, instances in new subnets in a custom VPC can communicate with each other across Availability Zones.

- **TRUE**
- FALSE



6. True or False: You can accelerate your application by adding a second internet gateway to your VPC.

- **FALSE**
- TRUE



7. When peering VPCs, you may peer your VPC only with another VPC in your same AWS account.

- **FALSE**
- TRUE



8. True or False: An application load balancer must be deployed into at least two subnets.

- **TRUE**
- FALSE



9. Which of the following is a chief advantage of using VPC endpoints to connect your VPC to services such as S3?

- **Traffic between your VPC and the other service does not leave the Amazon network.**
- VPC Endpoints offer a faster path through the public internet than you can realize with a NAT instance.
- VPC Endpoints require public IP addresses, offering rapid connectivity from the public internet.
- VPC endpoints are dedicated hardware devices that cannot be accessed without the correct IAM credentials.



10. Which of the following allows you to SSH or RDP into an EC2 instance located in a private subnet?

- **Bastion host**
- NAT instance
- NAT gateway
- Internet gateway



11. How many internet gateways can I attach to my custom VPC

- **1**
- 2
- 3
- One per Availability Zone.





12. You have five VPCs in a 'hub and spoke' configuration, with VPC 'A' in the center and individually paired with VPCs 'B', 'C', 'D', and 'E', which make up the 'spokes'. There are no other VPC connections. Which of the following VPCs can VPC 'B' communicate with directly?

- **VPC 'A'**
- VPCs 'A' and 'C'
- VPCs 'A' and 'E'
- VPCs 'C', 'D', and 'E'



13. Which of the following is true?

- **Security Groups are stateful and Network Access Control Lists are stateless.**
- Security Groups are stateless and Network Access Control Lists are stateful.
- Both Security Groups and Network Access Control Lists are stateless.
- Both Security Groups and Network Access Control Lists are stateful.



14. Which of the following offers the largest range of internal IP addresses?

- **/16**
- /28
- /24
- /20



15. Security groups act like a firewall at the instance level, whereas _________ are an additional layer of security that act at the subnet level.

- **Network ACLs**
- DB Security Groups
- VPC Security Groups
- Route Tables



16. In a default VPC, all Amazon EC2 instances are assigned two IP addresses at launch. What are they?

- **A private IP address & public IP address**
- A public IP address & secret IP address
- An Elastic IP address & public IP address
- An IPv6 address and Elastic IP address



17. When I create a new security group, all outbound traffic is allowed by default.

- TRUE
- FALSE



18. By default, how many VPCs am I allowed in each AWS region?

- 1
- 2
- 6
- **5**



19. Select the incorrect statement.

- In Amazon VPC, an instance retains its private IP.
- It is possible to have private subnets in a VPC.
- **In Amazon VPC, an instance does not retain its private IP.**
- You may have only 1 internet gateway per VPC.



20. To save administration headaches, a consultant advises that you leave all security groups in web-facing subnets open on port 22 to 0.0.0.0/0 CIDR. That way, you can connect wherever you are in the world. Is this a good security design?

- Yes.

- No.

  > 0.0.0.0/0 would allow ANYONE from ANYWHERE to connect to your instances. This is generally a bad plan. The phrase 'web-facing subnets' does not mean just web servers. It would include any instances in that subnet some of which you may not strangers attacking. You would only allow 0.0.0.0/0 on port 80 or 443 to to connect to your public facing Web Servers, or preferably only to an ELB. Good security starts by limiting public access to only what the customer needs. Please see the AWS Security whitepaper for complete details.