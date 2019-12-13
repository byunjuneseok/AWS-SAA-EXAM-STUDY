# Section 4 : EC2

 ## 23. EC2 101

### Pricing models.

**1. On Demand** : Allows you to pay a fixed rate by the hour (or by the second) with no long term commitment.

* Users that wnat the low cost and flexibility of EC2 without any up-front payment or long-term commitment.
* Applications with short term, spiky, or unpredictable workloads that can't be interrupted.

* Applications being developed or tested on EC2 for the first time.



**2. Reserved** : Provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract Terms are 1 Yr or 3Yr.

* Applications with steady state or predictable usage.
* Applications that require reserved capacity.
* Users able to make upfront payments to reduce their total computing costs even further.

*💵 Reserved Pricing Types*

1. Standard Reserved Instances

   > These offer up to 75% off on demand instances. The more you pay up front and the longer the contract, the greater the discount.

2. Convertible Reserved Instances

   > These offer up to 54% off on demand capability to change the attributes of th RI as long as the exchange results in the creation of Reserved Instances of equal or greater value.

3. Scheduled Reserved Instances

   > These are available to launch within the time windows you reserve. This option allows you to match your capacity reservation to a predictable recurrung schedule that only requires a fraction of a day, a week, or a month.





**3. Spot** : Enalbes you to bid whatever price you want for instance capicty, providing for even greater savings if your applications have flexible start and end times.

* Applications that have flexible start and end times.
* Applications that are only feasible at very low compute prices.
* Users with urgent computing needs for large amounts of additional capacity.

> If the spot instance is terminated by Amazon EC2, you won't be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.

Amazon EC2 스팟 인스턴스를 사용하면 AWS 클라우드에서 미사용 EC2 용량을 활용할 수 있습니다. 스팟 인스턴스는 온디맨드 요금과 비교하여 최대 90% 할인된 금액으로 제공됩니다. 빅 데이터, 컨테이너식 워크로드, CI/CD, 웹 서버, 고성능 컴퓨팅(HPC), 기타 테스트 및 개발 워크로드 등 다양한 상태 비저장, 내결함성 또는 유연한 애플리케이션에 스팟 인스턴스를 사용할 수 있습니다. 스팟 인스턴스는 Auto Scaling, EMR, ECS, CloudFormation, Data Pipeline 및 AWS Batch와 같은 AWS 서비스와 긴밀하게 통합되므로, 스팟 인스턴스에서 실행되는 애플리케이션을 시작하고 유지 관리하는 방법을 선택할 수 있습니다.

그뿐만 아니라 스팟 인스턴스를 온디맨드 및 RI와 손쉽게 결합하여 성능과 함께 워크로드 비용을 더욱 최적화할 수 있습니다. AWS의 운영 규모 덕분에 스팟 인스턴스는 대규모 워크로드를 실행할 수 있는 규모와 비용 절감을 제공할 수 있습니다. 또한, EC2에서 2분 알림을 통해 용량을 되돌리는 경우 스팟 인스턴스를 하이버네이트, 중단 또는 종료할 수 있는 옵션이 제공됩니다. 최대 90%의 할인된 금액으로 이렇게 방대한 규모로 미사용 컴퓨팅 용량에 손쉽게 액세스할 수 있는 것은 AWS가 유일합니다.  



**4. Dedicated Hosts** : Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licences.

* Useful for regulartory requirements that may not support multi-tenant virtualization.
* Great for licensing which does not support multi-tenancy or cloud deployments.
* Can be purchased On-Demand (hourly.)
* Can be purchased as a Reservation for up to 70% off the On-Demand price.

![image-20191210170345994](img/image-20191210170345994.png)

![image-20191210170805373](img/image-20191210170805373.png)

 

## 24 ~25 EC2 Hands on

### Exam tips

* Termination Protection is turned off by default, you must turn it on.
* On an EBS-backed instance, the dafult action is for the root EBS volume to be deleted when the instance is terminated.
* EBS Root Volumes of your default AMI's can be encrypted. You can also use a third party tool (such as bit locker etc) to encrypt the root volume, or this can be done when creating AMI's (lab to follow) in the AWS console or using the API.
* Additional volumes can be encrypted.



## 26. Security Group Basic

### Exam tips

* All inbound traffic is blocked by default.
* All outbound traffic is allowed.
* Changes to security group take effect immediately.
* You can have any number of EC2 instances within a security group.
* You can have multiple security groups attached to EC2 instances.
* Security groups are stateful.
* If you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again.
* You cannot block specific IP addresses using security groups, instead use Network Access Control List.
* You can speicify allow rules, but not deny rules.



## 27. EBS 101

Amazon Elastic Block Store provides presistent block storage volumes for use with Amazon EC2 instances in the AWS Cloud. Each Amazon EBS volume is automatically replicated within its Availability Zone to protect you from component failure, offering high availability and durability.

#### 5 Different Types of EBS Storage;

* General Purpose (SSD)

* Provisioned IOPS (SSD)

  > really-really fast.

* Throughput optimised Hard Disk Drive

* Cold Hard Disk Drive

* Magnetic

![image-20191213144258443](img/image-20191213144258443.png)

> *IOPS : Input Output Operation Per Second.*



## 28. Volumes & Snapshots

##### 참고

https://www.unixarena.com/2017/12/para-virtualization-full-virtualization-hardware-assisted-virtualization.html/

### Exam tips

* Volumes exist on EBS. (Think of EBS as a virtual hard disk)
* Snapshots exist on S3. Think of snapshots as a photograph of the disk.
* Snapshots are point in time copies of Volumes.
* **Snapshots are incremental** ; this means that only the blocks that have changed since your last snapshot are moved to S3.
* If this is your first snapshot, it may take some time to create.
* To create a snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot.
* However you can take a snap while the instance is running.
* You can create AMI's from both Volumes and Snapshots.
* You can change EBS volume sizes on the fly, including changing the size and storage type.
* **To move an EC2 volume from one AZ to another, take a snapshot of it, create an AMI from the snapshot and then use the AMI to launch the EC2 instance in a new AZ.**

* **To move an EC2 voluem from one region to another, take a snapshot of it, create an AMI from the snapshot and then copy the AMI from one region to the other. Then use the copied AMI to launch the new EC2 instance in the new region.**



## 29. AMI Types (EBS vs Instance Store)

