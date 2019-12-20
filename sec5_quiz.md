# Section 5 Quiz

1. Which of the following is not a feature of DynamoDB?

- The ability to perform operations by using a user-defined primary key.
- Data reads that are either eventually consistent or strongly consistent.
- The primary key can either be a single-attribute or a composite.
- **The ability to store relational-based data.**



2. What happens to the I/O operations of a single-AZ RDS instance during a database snapshot or backup?

- **I/O may be briefly suspended while the backup process initializes (typically under a few seconds), and you may experience a brief period of elevated latency.**
- Nothing.
- I/O operations to the database are sent to a secondary instance of a multi-AZ installation (for the duration of the snapshot.)
- I/O operations will function normally.



3. You can RDP or SSH into an RDS instance to see what is going on with the operating system.

- TRUE
- **FALSE**



4. AWS's NoSQL product offering is known as ________.

- RDS
- **DynamoDB**
- MongoDB
- MySQL



5. Which set of RDS database engines is currently available?

- Aurora, MySQL, SQL Server, Cassandra
- PostgreSQL, MariaDB, MongoDB, Aurora
- MariaDB, SQL Server, MySQL, Cassandra
- **Oracle, SQL Server, MySQL, PostgreSQL**



6. When creating an RDS instance, you can select the Availability Zone into which you deploy it.

- **TRUE**
- FALSE



7. RDS Reserved instances are available for multi-AZ deployments.

- TRUE
- FALSE



8. With new RDS DB instances, automated backups are enabled by default.

- **TRUE**
- FALSE



9. In RDS, what is the maximum value I can set for my backup retention period?

- 15 Days
- 30 Days
- **35 Days**
- 45 Days



10. If I wanted to run a database on an EC2 instance, which of the following storage options would Amazon recommend?

- RDS
- S3
- Glacier
- **EBS**



11. How many copies of my data does RDS – Aurora store by default?

- 3
- **6**
- 2
- 1



12. MySQL installations default to port number ________.

- 1433
- **3306**
- 3389
- 80



13. If you want your application to check RDS for an error, have it look for an ______ node in the response from the Amazon RDS API.

- Incorrect
- **Error**
- Abort
- Exit





14. Which of the following is most suitable for OLTP?

* **RDS**



15. Which of the following is most suitable for OLAP?

- ElastiCache
- RDS
- DynamoDB
- **Redshift**



16. Which AWS service is ideal for Business Intelligence Tools/Data Warehousing?

- Elastic Beanstalk
- ElastiCache
- DynamoDB
- **Redshift**



17. What data transfer charge is incurred when replicating data from your primary RDS instance to your secondary RDS instance?

- The charge is double the standard data transfer charge.
- The charge is the same as the standard data transfer charge.
- **There is no charge associated with this action.**
- The charge is half of the standard data transfer charge.



18. Under what circumstances would I choose provisioned IOPS over standard storage when creating an RDS instance?

- **If you use online transaction processing in your production environment.**
- If you have workloads that are not sensitive to latency/lag.
- If your business was trying to save money.
- If this was a test DB.



19. If you are using Amazon RDS Provisioned IOPS storage with a Microsoft SQL Server database engine, what is the maximum size RDS volume you can have by default?

- 500GB
- 1TB
- 32TB
- **16TB**
- 6TB



20. Which of the following AWS services is a non-relational database?

- RDS
- Redshift
- **DynamoDB**
- ElastiCache



21. You are hosting a MySQL database on the root volume of an EC2 instance. The database is using a large number of IOPS, and you need to increase the number of IOPS available to it. What should you do?

- Migrate the database to an S3 bucket.
- Migrate the database to Glacier.
- **Add 4 additional EBS SSD volumes and create a RAID 10 using these volumes.**
- Use CloudFront to cache the database.





22. In RDS, changes to the backup window take effect ________.

- After 30 minutes
- The next day
- Immediately
- You cannot back up in RDS





23. Amazon's ElastiCache uses which two engines?

- Redis & Memory
- Reddit & Memcrush
- **Redis & Memcached**
- MyISAM & InnoDB



24. When you add a rule to an RDS DB security group, you must specify a port number or protocol.

- TRUE
- **FALSE**

> Technically a destination port number is needed, however with a DB security group the RDS instance port number is automatically applied to the RDS DB Security Group.

