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

*WIP*