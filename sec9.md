# Section 9. Applications

## 85. SQS

Amazon SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them.

Amazon SQS is distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing.

 ![스크린샷 2019-12-26 오후 4.46.42](img/스크린샷 2019-12-26 오후 4.46.42.png)

> 이 상황에서 EC2 가 죽어도 새로운 EC2 가 만들어질때까지 데이터 SQS 에 대기



Using Amazon SQS, you can decouple the components of an application so they run independently, easing message management between components. Any component of a distributed application can stroe messages in a fail-safe queue. Messages can contain up to 256KB of text in any format. Any component can later retrieve the messages programmatically using the Amazon SQS API.

The queue acts as a buffer between the component producing and the component receiving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.

> intermittently : 간헐적으로 



### Two types of Queue.

* Standard Queues (default)

  Amazon SQS offers standard as the default queue type. A standard queue lets you have a nearly-unlimited number of transactions per second. Standard queues guarantee that a message is delivered at least once. However, occasionally (because of the highly-distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order. Standard queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent.

  ![스크린샷 2019-12-26 오후 5.10.59](img/스크린샷 2019-12-26 오후 5.10.59.png)



* Fifo Queues

  The Fifo queue complements the standard queue. The most important features of this queue type are FIFO (First in First out) delivery and exactly-once processing: The order in which messages are sent and received is strictly preserved and a message is delivered once and remains available until a consumer proccesses and deletes it; duplicates are not introduced into the queue.

  ![스크린샷 2019-12-26 오후 5.11.14](img/스크린샷 2019-12-26 오후 5.11.14.png)

 

### Exam Tips

* SQS is pull based, not pushed based.

* Messages are 256 KB in size.

* Messages can be kept in the queue from 1 minute to 14 days; the defualt retention period is 4 days.

* Visibility Time Out is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility time out expires, the message will then be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice.

* Visibility timeout maximum is 12 hours.

* SQS gurantees that your messages will be processed at least once.

* Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out.

  > Way of saving money.





## 86. SWF (Simple Work Flow service)

Amazon SWF is a web service that makes it easy to coordinate work across distributed application components. SWF enables applications for a range of use cases, including media processing, web application back-ends, business processworkflows, and analytics pipelines, to be designed as a coordination of tasks.

Tasks represent invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.

> Amazon Warehouse 에서 쓴다. "human element.."



### SWF vs SQS

* SQS hase a retention period of up to 14days, with SWF, workflow executions can last up to 1 yr.
* SWF presents a task-oriented API , whereas SQS ffers a message-oriented API.
* SWF ensures that a task is assigned only once and is never duplicated. With Amazon SQS, you need to handle duplicated messages and may also need to ensure that a message is processed only once.
* SWF keeps track of all the tasks and events in an aplication. With SQS, you need to implement your own application-level tracking, especially if your application uses multiple queues.



### Exam Tips

#### SWF Actor

* Workflow Starters - An Application that can inititate (start) a workflow. Could be your e-commerce website following the placement of an order, or a mobile app searching for bus times.
* Deciders - Control the flow of activity tasks in a workflow execution. If something has finished (or failed) in a workflow, a Decider decides what to do next.
* Activity Workers - Carry out the activity tasks.



## 87. SNS

Amazon SNS is a web service that makes it easy to set up, operate, and send notifications from the cloud. It provides developers with a highly scalable, felxible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.

Push notifications to Apple, Google, Fire OS, and Windows devices, as well as Android devices in China with Baidu Cloud Push.

Besides pushing cloud notifications directly to mobile devices, Amazon SNS can also deliver notifications by SMS text message or email to Amazon SQS queues, or to any HTTP endpoint.

SNS allows you to group multiple recipients using topics. A topic is an "access point" for allowing recipients to dynamically subscribe for identical copies of the same notification.

One topic can support deliveries to multiple endpoint types - for example, you can group together iOS, Android and SMS recipients. When you publish once to a topic, SNS delivers appropriately formatted copies of your message to each subscriber.

![스크린샷 2019-12-27 오후 3.48.19](img/스크린샷 2019-12-27 오후 3.48.19.png)

### SNS Benefits

* Instantaneous, push-based delivery (no polling)
* Simple APIs and easy integration with applications
* Flexible message delivery over multiple transport protocols
* Inexpensive, pay-as-you-go model with no up-front costs
* Web-based AWS Management Console offers the simplicity of a point-and-click interface



### Exam Tips

#### SNS vs SQS?

* Both Messaging Service in AWS
* SNS - PUSH
* SQS - POLLS (PULLS)



## 88. Elastic Transcoder

* Media Transcoder in the cloud.
* Convert media files from their original source format in to different formats that will play on smartphones, tablets, PCs, etc.
* Provides transcoding presets for popular output formats, which means that you don't need to guess about which settings work best on particular devices.
* Pay based on the minutes that you transcode and the resolution at which you transcode.

![스크린샷 2019-12-27 오후 3.52.35](img/스크린샷 2019-12-27 오후 3.52.35.png)



## 89. API Gateway

Fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale. With a few clicks in the AWS Management Console, you can create an API that acts as a "front door" for applicatiopns to acess data, business logic, or functionality from your back-end services, such as applications running on Amazon Elastic Compute Cloud (EC2), code running on AWS Lambda, or any web application.

![스크린샷 2019-12-27 오후 3.54.43](img/스크린샷 2019-12-27 오후 3.54.43.png)



### What Can API Gateway Do?

* Expose HTTPS endpoints to define a RESTful API

* Serverless-ly connect to services like Lambda & DynamoDB

* Send each API endpoint to a different target

* Run efficiently with low cost

* Scale effortlessly

* Track and control usage by API key

* Throttle requests to prevent attacks

* Connect to CloudWatch to log all requests for monitoring

* Maintain multiple versions of your API

  

### How Do I Configure API Gateway?

* Define an API (container)
* Define Resources and nested Resources (URL paths)
* For each resources: 
  * Select supported HTTP methods (verbs)
  * Set Security
  * Choose Target (Ec2, Lamda, DynamoDB, etc)
  * Set request and response transformations.



### How Do I Deploy API Gateway?

* Deploy API to a stage:
  * Uses API Gateway domain, by default.
  * Can use custom domain
  * Now supports AWS Certificate Manager : Free SSL/TLS Cert.



### Caching

You can enable API caching in Amazon API Gateway to cache your endpoint's response. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of the requests to your API. When you enable caching for a stage. API Gateway caches responsese from your endpoint for a specified time-to-live (TTL) period, in seconds. API Gateway then responds to the request by looking up the end point response from the cache instead of making a request to your endpoint.



### Same Origin Policy

In computing, the same-origin policy is an important concept in the web application security model. Under the policy, a web browser permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin.

This is done to prevent Cross-Site Scripting (XSS) attacks.

* Enforced by web browsers.
* Igonred by tools like PostMan and curl.



### CORS

Cors is one way the server at the other end (not the client code in the browser) can relax the same-origin policy. Cross-origin resources sharing (CORS) is a mechanism that allows restricted resources (eg fonts) on a web page to be requested from another domain outside the domain from which the first resource was served.  

* Browser makes an HTTP Options call for URL (Options is an HTTP method like GET, PUT, and POST)

* Server returns a response that says: 

  > "These other domains are approved to GET this URL."

* Error - "Origin Policy cannot be read at the remote resource?" You need to enable CORS on API Gateway.



### Exam Tips

* Remember what API Gateway is at a high level.
* API Gateway has caching capabilities to increase performance
* API Gateway is low cost and scales automatically
* You can throttle API Gateway to prevent attacks.
* You can log results to CloudWatch
* If you are using Javascript/AJAX that uses multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway.
* CORS is enforced by the client



## 90. Kinesis

### What is Streaming Data?

Streaming Data is data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously, and in small sizes. (order of Kilobytes)

* Purchases from online stores (amazon.com, kindle, ...)
* Stock Prices
* Game data (as the gamer plays)
* Social Network data
* Geospatial data (think uber.com, ..)
* IoT Sensor data



### Kinesis

Platform on AWS to sen your straming data to. Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for your business needs.

#### 3 Different Types of Kinesis

<img src="img/스크린샷 2019-12-27 오후 4.32.31.png" alt="스크린샷 2019-12-27 오후 4.32.31" style="zoom:50%;" />



##### Kinesis Streams

![스크린샷 2019-12-27 오후 4.33.53](img/스크린샷 2019-12-27 오후 4.33.53.png)

**Kinesis Streams Consist of Shards**;

* 5 transactions per second for reads, up to a maximum total data read rate of 2 MB per second and up to 1,000 records per second for writes, up to a maximum total data write rate of 1MB per second. (including partition keys.)
* The data capacity of your stream is a function of the number of shards that you specify for the stream. The total capacity of the stream is the sum of the capacities of its shards.



##### Kinesis Firehose - Redshift

![스크린샷 2019-12-27 오후 4.38.26](img/스크린샷 2019-12-27 오후 4.38.26.png)



##### Kinesis Firehose - Elasticsearch

![스크린샷 2019-12-27 오후 4.38.56](img/스크린샷 2019-12-27 오후 4.38.56.png)



### Exam Tips

* Know the difference between Streams and Firehose. You will be given scenario quesitons and you must choose the most relevant service.
* Understand what Kinesis Analytics is.

 



## 91. Web Identity Federation - Cognito

### Web Identity Federation

Web Identity Federation lets you give your users access to AWS resources after they have successfully authenticated with a web-based identity provider like Amazon, Facebook, or Google. Following successful authentication, the user receives an authentication code from the Web ID provider, which they can trade for temporary AWS security credentials.

### Amazon Cognito

Amazon Cognito provides Web Identity Federation with the following features;

* Sign-up and sign-in to your apps
* Access for guest users
* Acts as an Identity Broker between your application and Web ID providers, so you don't need to write any additional code.
* Synchronizes users data for multiple devices
* Recommended for all mobile applications AWS services.

#### Use Cases

* The recommended approach for web identity federation using social media accounts like facebook.

![스크린샷 2019-12-27 오후 4.55.28](img/스크린샷 2019-12-27 오후 4.55.28.png)

* Coginito borkers between the app and Facebook or Google to provide temporary credentials which map to an IAM role allowing access to the required resources. 
* No need for the application to embed or store AWS credentials locally on the device and it gives users  a seamless experience across all mobile devices.



#### Cognito User Pools

User Pools are user directories used to manage sign-up and sign-in functionality for mobile and web applications. Users can sign-in directly to the user Pool, or using Facebook, Amazon, or Google. Cognito acts as an Identity Broker between the identity provider and AWS. Successful authentication generates a JSON web token (JWTs).



#### Cognito Identity Pools

Identity pools enable provide temporary AWS credentials to access AWS services like S3 or DynamoDB.

![스크린샷 2019-12-27 오후 5.00.01](img/스크린샷 2019-12-27 오후 5.00.01.png)



#### Cognito Synchronisation

Cognito tracks the association between user identity and the various differnet devices they sign-in from. In order to provide a semaless user experience for your applications, Cognito uses Push Synchronization to push updates and synchronize user data accross multiple devices. Cognito uses SNS to send a notification to all the devices associated with a given user identity whenever data stored in the cloud changes.

![스크린샷 2019-12-27 오후 5.08.40](img/스크린샷 2019-12-27 오후 5.08.40.png)



### Cognito Exam Tips 

* Federation allows users to authenticate with a Web Identity Provider (Google, Facebook, Amazon)
* The users authenticateas first with the web ID Provider and receives and authentication token, which is exchanged for temporary AWS credentials allowing them to assume an IAM role.
* Cognito is an Identity Broker which handles interaction between your applications and the web ID provider (You don't need to write your own code to do this.)
* User pool is user based. It handles things like user registration, authentication, and account recovery.
* Identity pools authorise access to your AWS resources.



