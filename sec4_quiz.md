# QUIZ

1. Can Spread Placement Groups be deployed across multiple Availability Zones?

- **Yes.**
- Only in Us-East-1.
- Yes, but only using the AWS API.
- No.



2. When creating a new security group, all inbound traffic is allowed by default.

- TRUE
- **FALSE**



3. To help you manage your Amazon EC2 instances, you can assign your own metadata in the form of ________.

- Wildcards
- Certificates
- **Tags**
- Notes



4. Which of the following features only relate to Spread Placement Groups?

- Instances must be deployed in a single Availability Zone.
- The name of your placement group must be unique within your AWS Account.
- **The placement group can only have 7 running instances per Availability Zone.**
- There is no charge for creating a placement group.



5. In order to enable encryption at rest using EC2 and Elastic Block Store, you must ________.

- **Configure encryption when creating the EBS volume**

- Configure encryption using the appropriate Operating Systems file system

- Configure encryption using X.509 certificates

- Mount the EBS volume in to S3 and then encrypt the bucket using a bucket policy

  > The use of encryption at rest is default requirement for many industry compliance certifications. Using AWS managed keys to provide EBS encryption at rest is a relatively painless and reliable way to protect assets and demonstrate your professionalism in any commercial situation.



6. Can I move a reserved instance from one region to another?

- Yes.

- **No.**

- It depends on the region.

- Only in the US.

  > Depending on you type of RL you can You can modify the AZ, scope, network platform, or instance size (within the same instance type), but not Region. In some circumstances you can sell RIs, but only if you have a US bank account.



7. You need to know both the private IP address and public IP address of your EC2 instance. You should ________.

- Run IPCONFIG (Windows) or IFCONFIG (Linux)

- **Retrieve the instance Metadata from http://169.254.169.254/latest/meta-data/**

- Retrieve the instance User Data from http://169.254.169.254/latest/meta-data/

- Use the following command: AWS EC2 DisplayIP

  > Instance Metadata and User Data can be retrieved from within the instance via a special URL. Similar information can be extracted by using the API via the CLI or an SDK.



8. Amazon's EBS volumes are ________.

- Object-based storage
- **Block-based storage**
- Encrypted by default
- Not suitable for databases



9. If an Amazon EBS volume is an additional partition (not the root volume), can I detach it without stopping the instance?

- **Yes, although it may take some time.**
- No, you will need to stop the instance.



10. You can add multiple volumes to an EC2 instance and then create your own RAID 5/RAID 10/RAID 0 configurations using those volumes.

- **TRUE**
- FALSE



11. Individual instances are provisioned ________.

- In Regions
- **In Availability Zones**
- Globally



12. Spread Placement Groups can be deployed across multiple Availability Zones

- **TRUE**

- FALSE

  > Spread Placement Groups can be deployed across availability zones since they spread the instances further apart. Cluster Placement Groups can only exist in one Availabiity Zone since they are focused on keeping instances together, which you cannot do across Availability Zones



13. Is it possible to perform actions on an existing Amazon EBS Snapshot?

- **Yes, through the AWS APIs, CLI, and AWS Console.**
- No.
- It depends on the region.
- EBS does not have snapshot functionality.





14. 🤔 You have developed a new web application in the US-West-2 Region that requires six Amazon Elastic Compute Cloud (EC2) instances to be running at all times. US-West-2 comprises three Availability Zones (us-west-2a, us-west-2b, and us-west-2c). You need 100 percent fault tolerance: should any single Availability Zone in us-west-2 become unavailable, the application must continue to run. How would you make sure 6 servers are ALWAYS available? NOTE: each answer has 2 possible deployment configurations. Select the answer that gives TWO satisfactory solutions to this scenario.

- Solution 1: us-west-2a with two EC2 instances, us-west-2b with two EC2 instances, and us-west-2c with two EC2 instances. Solution 2: us-west-2a with six EC2 instances, us-west-2b with six EC2 instances, and us-west-2c with no EC2 instances.

- **Solution 1: us-west-2a with six EC2 instances, us-west-2b with six EC2 instances, and us-west-2c with no EC2 instances. Solution 2: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances.**

- Solution 1: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with no EC2 instances. Solution 2: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances.

- Solution 1: us-west-2a with three EC2 instances, us-west-2b with three EC2 instances, and us-west-2c with three EC2 instances. Solution 2: us-west-2a with four EC2 instances, us-west-2b with two EC2 instances, and us-west-2c with two EC2 instances.

  > You need to work through each case to find which will provide you with the required number of running instances even if one AZ is lost. Hint: always assume that the AZ you lose is the one with the most instances. Remember that the client has stipulated that they MUST have 100% fault tolerance.



15. The use of a cluster placement group is ideal _______.

- When you need to distribute content on a CDN network

- When you need to deploy EC2 instances that require high disk IO

- Your fleet of EC2 Instances requires low latency and high network throughput across multiple availability zones

- **Your fleet of EC2 instances requires high network throughput and low latency within a single availability zone**

  > Cluster Placement Groups are primarily about keeping you compute resources within one network hop of each other on high speed rack switches. This is only helpful when you have compute loads with network loads that are either very high or very sensitive to latency.



16. EBS Snapshots are backed up to S3 in what manner?

- **Incrementally**
- Exponentially
- Decreasingly
- EBS snapshots are not stored on S3.



17. Can I delete a snapshot of an EBS Volume that is used as the root device of a registered AMI?

- **No.**
- Yes.
- Only via the Command Line.
- Only using the AWS API.



18. Which AWS CLI command should I use to create a snapshot of an EBS volume?

- **aws ec2 create-snapshot**
- aws ec2 fresh-snapshot
- aws ec2 deploy-snapshot
- aws ec2 new-snapshot



19. I can change the permissions of a role, even if that role is already assigned to an existing EC2 instance, and these changes will take effect immediately.

- **TRUE**
- FALSE



20. I can change the permissions of a role, even if that role is already assigned to an existing EC2 instance, and these changes will take effect immediately.

- **TRUE**
- FALSE



21. Will an Amazon EBS root volume persist independently from the life of the terminated EC2 instance to which it was previously attached? In other words, if I terminated an EC2 instance, would that EBS root volume persist?

- Yes.

- No.

- **Only if I specify (using either the AWS Console or the CLI) that it should do so.**

- It depends on the region in which the EC2 instance is provisioned.

  > You can control whether an EBS root volume is deleted when its associated instance is terminated. The default delete-on-termination behaviour depends on whether the volume is a root volume, or an additional volume. By default, the DeleteOnTermination attribute for root volumes is set to 'true.' However, this attribute may be changed at launch by using either the AWS Console or the command line. For an instance that is already running, the DeleteOnTermination attribute must be changed using the CLI.



22. I can use the AWS Console to add a role to an EC2 instance after that instance has been created and powered-up.

- **TRUE**
- FALSE



23. Can you attach an EBS volume to more than one EC2 instance at the same time?

- Yes.
- **No.**
- If that EC2 volume is part of an AMI.
- Depends on which region.