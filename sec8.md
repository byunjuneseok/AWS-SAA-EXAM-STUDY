

# Section 8. HA. Architecture

## 73. Load Balancers Theory

### Load Balancer Types

1. **Application Load Balancer**

   Best suited for load balancing of HTTP / HTTPS traffic. They operate at Layer 7 and are application-aware. They are intelligent, and you cna create advanced request routing, sending specified requests to specific web servers.

   

2. **Network Load Balancer**

   Best suited for load balancing of TCP traffic where extreme performance is required. Operating at the connection level (Layer 4), Network load balancer are capable of handling millions of requests per second, while maintaining ultra-low latencies.

   *Use for extreme performance!*

   

3. **Classic Load Balancer**

   The legacy Elastic Load Balancers. You can load balance HTTP/HTTPS applications and use Layer 7-specific features, such as X-Forwarded and sticky sessions. You can also use strict Layer 4 loadbalancing for applications that they rely purely on the TCP protocol.

   If your application stops responding, the ELB (Classic Load Balancer) responds with a 504 error. This means that the application is having issues. This could be either at the web server layer or at the database layer. Identify where the application is failing, and sclae it up or out where possible.



### X-Forwarded-For Header

![스크린샷 2019-12-24 오후 3.09.47](img/스크린샷 2019-12-24 오후 3.09.47.png)

If you need the IPv4 address of your end user, look for the **X-Forwarded-For** header.



### Exam Tips

* 504 Error means the gateway has timed out. This means that the application not responding within the idle timeout period.
* Troubleshoot the application. Is it the web server or database server?
* If you need the IPv4 address of your end user, look for the **X-Forwarded-For** header.



## 74. Load Balancer & Health Checks

 ### Exam Tips

* Instances monitored by ELB are reported as `InService`, or `OutofService`
* Health Checks check the instance health by talking to it.
* Load Balances have their own DNS name. You are never given an IP address.
* Read the ELB FAQ for Classic Load Balancers.



## 75. Advanced Load Balancer Theory

### What are STICKY SESSIONS?

Classic Load Balancer routes each request independently to the registered EC2 instance with the smallest load.

Sticky sessions allow you to bind a user's session to a specific EC2 instance. This ensures that all requests from the user during the session are sent to the same instance.

You can enable Sticky Sessions for Application Load Balancers as well, but the traffic will be sent at the Target Group Level.

### What is Cross Zone Load Balancing

#### No Cross Zone Load Balancing

![스크린샷 2019-12-24 오후 3.34.47](img/스크린샷 2019-12-24 오후 3.34.47.png)



#### With Cross Zone Load Balancing

![스크린샷 2019-12-24 오후 3.35.34](img/스크린샷 2019-12-24 오후 3.35.34.png)



#### Common EXAM Scenario

![스크린샷 2019-12-24 오후 3.36.21](img/스크린샷 2019-12-24 오후 3.36.21.png)



### What are Path Patterns?

You can create a listener with rules to forward requests based on the URL path. This is known as path-based routing. If you are running microservices, you can route traffic to multiple back-end services using path-based routing. For example, you can route general requests to one target group and requests to render images to another target group.

#### Common EXAM Scenario

![스크린샷 2019-12-24 오후 3.39.29](img/스크린샷 2019-12-24 오후 3.39.29.png)



### Exam Tips

* Sticky Sessions enable your users to stick to the same EC2 instance. Can be useful if you are storing information locally to that instance.
* Cross Zone Load Balancing enables you to load balance across multiple AZ.
* Path patterns allow you to direct traffic to different EC2 instances based on the URL contained in the request.



## 76. Autoscaling Groups

https://docs.aws.amazon.com/autoscaling/ec2/userguide/control-access-using-iam.html



## 77. HA Architecture

> High Availability

### Plan For Failure

*"Everything fails, Everything! You should always plan for failure."*

<img src="img/스크린샷 2019-12-26 오전 10.45.33.png" alt="스크린샷 2019-12-26 오전 10.45.33" style="zoom:33%;" />

### HA Architecture EXAMPLE

![스크린샷 2019-12-26 오전 10.48.14](img/스크린샷 2019-12-26 오전 10.48.14.png)

### HA Sample Exam Question

**Scenario : You have a website that requires a minimum of 6 instances and it must be highly available. You must also be able to tolerate the failure of 1 AZ. What is the ideal architecture for this environment while also being the most cost effective?**

* 2 AZs with 2 instances in each AZ.
* **3 AZs with 3 instances in each AZ.**
* 1 AZ with 6 instances in each AZ.
* 3 AZs with 2 instances in each AZ.



### Exam Tips

* Always Design for failure.

* Use Multiple AZ's and Multiple Regions where ever you can.

* Know the difference between Multi-AZ and Read Replicas for RDS.

* Know the difference between scaling out and scaling up. 

  > scaling out : EC2 개수
  >
  > scaling up : t2micro -> 더 큰거..

* Read the question carefully and always consider the cost element.

* Know the different S3 storage classes.





## 78-82.

<img src="img/스크린샷 2019-12-26 오전 10.55.58.png" alt="스크린샷 2019-12-26 오전 10.55.58" style="zoom:33%;" />



![스크린샷 2019-12-26 오후 12.08.31](img/스크린샷 2019-12-26 오후 12.08.31.png)





### Exam Tips

* CloudFormation
  * Is a way of completely scripting your cloud environment.
  * Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly.



## 83. Elastic Beanstalk

With Elastic Beanstalk, you can quickly deploy and manage appications in the AWS Cloud without worrying about the infrastructure that runs those applications. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.

