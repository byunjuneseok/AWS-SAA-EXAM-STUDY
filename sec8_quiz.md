# QUIZ

1. You have a website with three distinct services, each hosted by different web server autoscaling groups. Which AWS service should you use?

- S3 static websites
- Elastic Load Balancers (ELB)
- **Application Load Balancers (ALB)**
- Classic Load Balancers (CLB)
- Network Load Balancers (NLB)

> The ALB has functionality to distinguish traffic for different targets (mysite.co/accounts vs. mysite.co/sales vs. mysite.co/support) and distribute traffic based on rules for target group, condition, and priority.



2. You manage a high-performance site that collects scientific data using a bespoke protocol over TCP port 1414. The data comes in at high speed and is distributed to an autoscaling group of EC2 compute services spread over three AZs. Which type of AWS load balancer would best meet this requirement?

- CloudFront combined with Lambda@Edge
- Elastic Load Balancers (ELB)
- Application Load Balancers (ALB)
- **Network Load Balancers (NLB)**



3. You have been tasked with creating a resilient website for your company. You create the Classic Load Balancer with a standard health check, a Route 53 alias pointing at the ELB, and a launch configuration based on a reliable Linux AMI. You have also checked all the security groups, NACLs, routes, gateways and NATs. You run the first test and cannot reach your web servers via the ELB or directly. What might be wrong?

- **The launch configuration is not being triggered correctly.**
- The health check is not set up correctly.
- Your autoscaling group is set to zero instances.
- You have specified the wrong key pair and the servers cannot start the http service properly.

> In a question like this you need to evaluate if all the necessary services are in place. The glaring omission is that you have not built an autoscaling group to invoke the launch configuration you specified. The instance count and health check depend on instances being created by the autoscaling group. Finally, key pairs have no relevance to services running on the instance.



4. If you are told that an EC2 instance is being changed to have more RAM, Is this considered scaling up or scaling out

- Scaling out
- **Scaling up**



5. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that you can access a resource or service when you need it?

- **Availability**
- Durability
- Resiliency
- Reliability



6. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that a resource will continue to exist until you decide to remove it?

- Availability
- **Durability**
- Resiliency
- Reliability



7. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that a resource ability to recover from damage or disruption?

- Availability
- Durability
- **Resiliency**
- Reliability



8. In discussions about cloud services the words 'availability', 'durability', 'reliability' and 'resiliency' are often used. Which term is used to refer to the likelihood that a resource will work as designed?

- Availability
- Durability
- Resiliency
- **Reliability**



9. You work for a major news network in Europe. They have just released a new mobile app that allows users to post their photos of newsworthy events in real-time. Your organization expects this app to grow very quickly, essentially doubling its user base each month. The app uses S3 to store the images, and you are expecting sudden and sizable increases in traffic to S3 when a major news event takes place (as users will be uploading large amounts of content.) You need to keep your storage costs to a minimum, and you are happy to temporally lose access to up to 0.1% of uploads per year. With these factors in mind, which storage media should you use to keep costs as low as possible?

- **S3 Standard-IA**
- S3 Standard
- S3 – OneZone-Infrequent Access
- S3 – Reduced Redundancy Storage (RRS)
- Glacier
- S3 – Provisioned IOPS



10. You work for a manufacturing company that operate a hybrid infrastructure with systems located both in a local data center and in AWS, connected via AWS Direct Connect. Currently, all on-premise servers are backed up to a local NAS, but your CTO wants you to decide on the best way to store copies of these backups in AWS. He has asked you to propose a solution which will provide access to the files within milliseconds should they be needed, but at the same time minimizes cost. As these files will be copies of backups stored on-premise, availability is not as critical as durability. Choose the best option from the following which meets the brief.

- Copy the files from the NAS to an S3 bucket configured as Standard class.
- Copy the files to an EC2 instance with a large EBS volume attached.
- **Copy the files from the NAS to an S3 bucket with the One Zone-IA class**
- Copy the files from the NAS to an S3 bucket with the Reduced Redundancy Storage class.



11. You need to use an object-based storage solution to store your critical, non-replaceable data in a cost-effective way. This data will be frequently updated and will need some form of version control enabled on it. Which S3 storage solution should you use?

- **S3**
- S3 – IA
- S3 – OneZone-IA
- S3 – RRS
- Glacier



12. In S3 the durability of my files is ________.

- 99.99%
- 99.999999999%
- 99%
- 100%



13. When you have deployed an RDS database into multiple availability zones, can you use the secondary database as an independent read node?

- **No.**
- Only in US-West-1.
- It depends on how you set it up.
- Yes.



14. Placement groups can either be of the type 'cluster', 'spread', or 'partition'. Choose options from below which are only specific to Spread Placement Groups.

- Spread placement groups require a name that is unique within your AWS account for the region.
- An instance can be launched in one placement group at a time and cannot span multiple placement groups.
- A spread placement group is a logical grouping of instances within a single Availability Zone.
- **A spread placement group is a group of instances that are each placed on distinct underlying hardware.**



15. Can I "force" a failover for any RDS instance that has multi-AZ configured?

- **Yes.**
- No.
- Only for Oracle RDS instances.

