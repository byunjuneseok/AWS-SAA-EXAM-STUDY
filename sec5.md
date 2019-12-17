#  Section 5. Databases on AWS

## 41. Database 101

### What is a realational database? 

Relational databases are what most of use are all used to. They have been around since thew 70's. Think of a *traditional spreadsheet*:

* Database
* Tables
* Row
* Fields (Columns)

#### Relational databases on AWS;

* SQL Server
* Oracle
* MySQL Server
* PostgreSQL
* Aurora
* MariaDB

#### RDS has two key features;

* Multi-AZ - For Disaster Recovery

  > 아마존이 DNS 레코드를 호스트하고 AZ1의 Primary Database 를 포인트를 한다고 가정. AZ1 에 있는 Primary Database 가 터졌을때 아마존이 이를 인지하고, AZ2 에 있는 Secondary Database 를 포인트함.

* Read Replicas - For Performance

  > AZ1 의 Primary Database 에 데이터를 쓰게 된다면, 바로 AZ2의 Read Replica 에 복제된다. "perfect copy" Primary Database 가 터졌을 때, 새로운 url 을 사용해야 한다.



### Non Relational Databases

#### Non Relational Databases are as follows;

* Collection *= Table*
* Document = *Row*
* Key Value Pairs = *Fields*



### What is Data Warehousing?

Used for business intelligence. Tools like Cognos, Jaspersoft, SQL Server Reporting Services, Oracle Hyperion, SAP NetWeaver.

Used to pull in very large and complex data sets. Usually used by management to do queries on data (such as current performance vs targets etc)



#### OLTP vs OLAP

Online Transaction Processing (OLTP) differs from OLAP Online Analytic Process (OLAP) in terms of the types of queries you will run.

**OLTP EXAMPLE:**

Pulls up a row of data such as Name, Date, Address to Deliver to, Delivery Status etc.

> Order number 2120121



**OLAP transaction Example:**

Pulls in large numbers of records.

> Net Profit for EMEA and Pacific for the Digital Radio Product.
>
> Sum of Radios Sold in EMEA.
>
> Sum of Radios Sold in Pacific.
>
> Unit Costs of Radio in each region 
>
> Sales price of each radio.
>
> Sales price - unit costs



Data Warehousing databases use different type of architecture both from a database perspective and infrastructure layer. 

👉 **Amazon's Data Warehouse Solution is called Redshift.**



> **참고** 
>
> OLTP 란 온라인 트랜잭션 처리를 말하며, 네트워크 상의 온라인 사용자들의 Database 에 대한 일괄 트랜잭션 처리를 의미한다. 
>
> 흔히 말하는 "트랜잭션(Transaction) 처리" 를 OLTP 라 부른다. 트랜잭션이라 부르는 용어의 의미 자체가 OLTP 의 의미를 포함하고 있다고 할 수 있겠다. 
>
> 트랜잭션의 주 특징은 그루핑된 연산의 실패시, Rollback 이 지원된다는 점이다.
>
> 주로 기술적 특성상, 대규모의 처리보다는 소규모의 정교한 데이터 구성이 필요한 데이터의 처리가 중점이 된다.
>
> 
>
>  OLAP 란 Database 자체적으로 운용되는 시스템이라기 보다는 데이터 웨어하우스 등의 시스템과 연관되어 Data 를 분석하고 의미있는 정보로 치환하거나, 복잡한 모델링을 가능하게끔 하는 분석 방법을 말한다.
>
> 기능 자체에 중심을 두는 OLTP 와는 다르게 사용하는 목적과 주제에 보다 중점을 둔다.
>
> 그렇기 때문에 주로 대용량의 데이터에 대해 처리하고 보다 복잡한 Data processing 으로 의미를 추출하는데 중점을 둔다.



### What is EleastiCache?

ElastiCache is a web service that makes it easy to deploy, operate, and scale and in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

ElastiCache supports two open-source in-memory caching engines:

* Memcached
* redis



### Exam Tips

#### RDS (OLTP)

* SQL
* MySQL
* PostgresQL
* Oracle
* Aurora
* MariaDB

#### DynamoDB (NoSQL)

#### Red Shift OLAP

#### ElastiCache : to speed up performance of existing databases (frequent identical quries.)

* Memcached
* Redis

#### Redsihift for business intelligence or data warehousing





## 42. Let's create an RDS instance.

![스크린샷 2019-12-17 오후 4.06.35](img/스크린샷 2019-12-17 오후 4.06.35.png)

```bash
#!/bin/bash
yum install httpd php php-mysql -y
cd /var/www/html
wget https://wordpress.org/wordpress-5.1.1.tar.gz
tar -xzf wordpress-5.1.1.tar.gz
cp -r wordpress/* /var/www/html/
rm -rf wordpress
rm -rf wordpress-5.1.1.tar.gz
chmod -R 755 wp-content
chown -R apache:apache wp-content
service httpd start
chkconfig httpd on%
```

> Bootstrap code.

 

### Remember the following points;

* RDS runs on virtual machines.
* You can't login to these os however.
* Patching of the RDS Operating System and DB is Amazon's responsibility.
* RDS is NOT Serverless.
* Aurora Serveless is SERVERLESS.



## 43. RDS Backups, Multi-AZ & Read Replicas

### Two different types of Backups for RDS:

* Automated Backups
* Database Snapshots

#### Automated Backups

Allow you to recover your database to any point in time within a ***retention period*.** The retention period can be between one and 35 days. Automated Backups will take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will first choose the most recent daily backup, and then apply transaction logs relevant to that day. This allows you to do a point in time recovery down to a second, within the retension period.

Automated Backups are enabled by default. The backup data is stored in S3 and you get free storage space equal to the size of your database. So if you have an RDS instance of 10GB, you will get 10Gb worth of storage.

Backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is being backed up and you mayexperience elevated latency.

#### Database Snapshots

done manually. (ie they are user initiated.) They are stored even after you delete the original RDS instance, unlike automated backups.

Whenever you restore either an Automatic Backup or a manual Snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint.



### Encrpytion At Rest

Encrpytion at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS KMS (Key Management Service) Service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.



###What is Multi-AZ.

Multi-AZ allows you to have an exact copy of your production database in another AZ. AWS handles the replication for you, so when your production database is written to, this write will automatically be synchronized to the stand by database.

In the event of planned database maintenance, DB Instance failure, or an AZ failure, Amazon RDS will automatically failover to the standby so that database operations can resume quickly without administrative intervention.

**MULTI-AZ is for DISASTER RECOVERY ONLY**

It's not primarily used for improving performance. For performance improvement, you need Read Replicas.

#### Multi-AZ Support

* SQL Server
* Oracle
* MySQL Server
* PostgreSQL
* MariaDB





### What is A Read Replica

<img src="img/스크린샷 2019-12-17 오후 4.51.10.png" alt="스크린샷 2019-12-17 오후 4.51.10" style="zoom:50%;" />

Production DB asynchronously replicating out to multiple copies.



<img src="img/스크린샷 2019-12-17 오후 4.52.31.png" alt="스크린샷 2019-12-17 오후 4.52.31" style="zoom: 50%;" />

EC2 instances read from diffrent READ-REPLICAS and only write to single database. Of course, it replicate out to read-replicas.

![스크린샷 2019-12-17 오후 4.54.35](img/스크린샷 2019-12-17 오후 4.54.35.png)

READ REPLICAS OF READ REPLICAS.



Read replicas allow you to have a read-only copy of your production database. This is achieved by using Asynchronous replication from the primary RDS instance to read replica. You use read replicas primarily for very read-heavy database workloads.



자주 출제되는 것. 데이터베이스의 성능을 올릴 수 있는 두 가지 방법.

* Read Replicas 만들기
* ElastiCache 사용하기

#### Read Replicas Support

* Oracle
* MySQL Server
* PostgreSQL
* MariaDB
* Aurora



#### Things to know about Read Replicas;

* Used for scaling, not for DR!
* Must have automatic backups turned on in order to deploy a read replica.
* You can have up to 5 read replica copies of any database.
* You can have read replicas of readreplicas (but watch out for latency.)
* Each read replica will have its own DNS end point.
* You can have read replicas that have Multi-AZ.
* You can create read replicas of Multi-AZ source databases.
* Read replicas can be promoted to be their own databases. This breaks the replication.
* You can have a read replicaa in a second region.



## 44. RDS Backups, Multi-AZ & Read Replicas - Lab

### Exam Tips

#### There are two differnet types of Backups for RDS:

* Autiomated Backups
* Database snapshots



#### Read Replicas

* Can be Multi-AZ.
* Used to increase performance.
* Must have backups turned on.
* Can be in defferent regions.
* Can be MySQL, PostgreSQL, MariaDB, Oracle, Aurora.
* Can be promoted to master, this will break the read replica.



#### Multi-AZ

* Used for DR. (Disaster Recovery.)
* You can force a failover from one AZ to another by rebooting the RDS instance.



#### Encryption

Encrpytion at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS KMS (Key Management Service) Service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.



## 45. DynamoDB

Amazon DynamoDB is a fast and flexible **NoSQL** database service for all aplications that need consistent, single-digit millisecond latency at any scale. It's a fully managed database and supports both document and key-value data models. It's flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

* Stored on SSD storage.
* Spread accross 3 geographically disntinct data centers.
* Eventual Consistent Reads. (Default)
* Strongly Consistent Reads.



### DynamoDB reads.

#### Eventual Consisstnet Reads.

* Consistency across all copies of data is usually reached witihin a second. Repeating a read after a short time should return rhe updated data. (Best Read Performance)

#### Strongly Consistent Reads

* A Strongly consistent read returns a result that reflects all writes that received a successful response prior to the read.



### Exam Tips

* Stored on SSD storage.
* Spread accross 3 geographically disntinct data centers.
* Eventual Consistent Reads. (Default)
* Strongly Consistent Reads.





## 46. Redshift

Amazon Redshift is a fast and powerful, fully managed, petabyte-scale data warehouse service in the cloud. Customers can start small for just \$0.25 per hour with no commitments or upfront costs and scale to a petabyte or more \$1,000 per terabyte per year, less than a tenth of most orher data warehousing solutions.

Data Warehousing databases use different type of architecture both from a database perspective and infrastructure layer.



### Redshift Configuration

* Single Node (160GB)
* Multi-Node
  * Leader Node (manages client connections and receives queries.)
  * Compute Node (store data and perform queries and computations). Up to 128 Compute nodes.



#### Advanced compression

Columnar data stores can be compressed much more than row-based data stores because siliar data is stored sequentially on disk. Amazon Redshift employs multiple compression technique and can often archieve significant compression relatvice to trational relational data stores. In addition, Amazon Redshift doesn't require indexes or materialized views, and so uses less space than traditional relational database systems. When loading data into an empty table, Amazon Redshift automaticaclly samples your data and selects the most appropriate compression scheme.



#### MPP (Massively Parallel Proccessing)

Amazon Redshift automatically distributes data and query load across all nodes. Amazon Redshift make it easy to add nodes to your data warehouse and enables you to maintain fast query performance as your data warehouse grows.



#### Backups

* Enabled by default with a 1 day retention period.
* Maximum retention period is 35 days.
* Redshift always attempts to maintain at least three copies of your data (the original and replica on the compute nodes and a backup in Amazon S3).
* Redshift can also asynchronously replicate your snapshots to S3 in another region for disaster recovery.



#### Redshift is priced as folows;

* Compute Node Hours (total number of hours you run across all your compute nodes for the billing period. You are billed for 1 unit per node per hour, so a 3-node data warehouse cluster running persistently for an entire month would incur 2,160 instance hours. You will not be charged for leader node hours; only compute node will incur charges.)



#### Security Considerations:

* Encrypted in transit using SSL.

* Encrypted at rest using AES-256 encryption.

* By default RedShift takes care of key management.

  * Manage your own keys through HSM
  * AWS Key Management Service

  

  

#### Redshift Availability

* Currently only available in 1 AZ
* Can restore snapshots to new AZs in the event of an outage.





### Exam Tips

* Redshift is used for business intelligence.
* Available in only 1 AZ



#### Backups

* Enabled by default with a 1 day retention period.
* Maximum retention period is 35 days.
* Redshift always attempts to maintain at least three copies of your data (the original and replica on the compute nodes and a backup in Amazon S3).
* Redshift can also asynchronously replicate your snapshots to S3 in another region for disaster recovery.



## 47. Aurora

MySQL - compatible, relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open source databases. Amazon Aurora provides up to five times better performance than MySQL at a price point one tenth that of a commercial database while delivering similar performance and availability.

> 아마존은 build aurora from scratch.. mySQL 뿐만 아니라 postgresql 과 호환.



### Things to know about Aurora;

* Start with 10GB, scales in 10GB increments to 64TB (Storage Autoscaling.)
* Compute resources can scale up to 32vCPUs and 244GB of Memory.
* 2 copies of your data is contained in each AZ, with minimum of 3 AZ. 6 copies of your data.



### Scaling Aurora

* Aurora is designed to transparently handle the loss of up to two copies of data without affecting database write availability and up to three copies without affecting read availability.
* Aurora storage is also self-healing. Data blocks and disks are continueously scanned for errors and repaired automatically.



### Two types of Aurora Replicas are available;

* Aurora Replicas (currently 15)
* MySQL Read Replicas (currently 5)

![스크린샷 2019-12-17 오후 9.37.08](img/스크린샷 2019-12-17 오후 9.37.08.png)

> Automated Failover!

 

#### Backups with Aurora

* Automated backups are always enabled on Amazon Aurora DB Instances. Backups do not impact database performance.
* You can also take snapshots with Aurora. This also does not impact on performance.
* You can share Aurora snapshots with other AWS account.



### Exam Tips

* 2 Copies of your data is contained in each AZ, with minimum of 3 AZ. 6 copies of your data.
* You can share Aurora Snapshots with other AWS accounts.
* 2 types of replicas available. Aurora Replicas and MySQL replicas. Automated failover is only available with Aurora Replicas.
* Aurora has automated backups turned on by default. You can also take Snapshots with Aurora. You can share these snapshots with other AWS accounts.





## 48. ElastiCache

ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the clouds. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

* MEMCACHED

* redis

  ![스크린샷 2019-12-17 오후 9.49.12](img/스크린샷 2019-12-17 오후 9.49.12.png)

### Exam Tips

* Use Elasticache to increase database and web application performance.
* Redis is Multi-AZ
* You can do backups and restores of Redis.

