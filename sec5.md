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











 

