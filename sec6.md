# Section 6. Route53

## 51. DNS 101

### IPv4 vs IPv6

#### IPv4 Addresses are running out...

* IPv4 : 4 Billion
* IPv6 : 340undecillion

### Top Level Domains

`.com`, `.edu`, `.gov`, `co.uk`, ...

* `co.uk` : `uk` 는 top level domain, `co`는 second level domain name.
* IANA (Internet Assigned Numbers Authority)



### Domain Registrars

Because all of the names in a given domain name have to be unique there needs to be a way to organize this all so that domain names aren't duplicated. This is where domain registrars come in. A registrar is an authority that can assign domain names directly under one or more top-level domains. These domains are registered with InterNIC, a service of ICANN, which enforces uniqueness of domain names across the internet. Each domain name becomes registered in a central database known as the WhoIS database.

Popular domain registrars include Amazon, GoDaddy.com, 123-reg.co.uk etc.



### Start of Authority Record (SOA)

**SOA record stores information about:** 

* The name of the server that supplied the data for the zone.
* The administrator of the zone.
* The current version of the data file.
* The default number of seconds for the time-to-live file on resource records.





### NS Records

**NS stands for Name Server Records**

They are used by Top Level Domain servers to direct traffic to the Content DNS server which contains the authoritative DNS records.

![스크린샷 2019-12-20 오후 3.46.18](/Users/byun/Library/Application Support/typora-user-images/스크린샷 2019-12-20 오후 3.46.18.png)



### A record?

An "A" record is the fundamental type of DNS record. The "A" in A record stands for "Address". The A record is used by a computer to translate the name of the domain to an IP address.



### TTL

The length that a DNS record is cached on either the Resolving Server or the users own local PC is equal to the value of the TTL (Time to live) in seconds. The lower the time to live, the faster changes to DNS records take to propagate throughout the internet.



### CName

A Canonical Name (CNAME) can be used to resolve one domain name to another. For example, you may have a mobile website with the domain name `http://m.acloud.guru` that is used for when users browse to your domain name on their mobile devices. You may also want the name `http://mobile.acloud.guru` to resolve to this same address.



### Alias

Alias records are used to map resource record set in your hosted zone to Elastic Load Balancers, Cloud distributions, or S3 buckets that are configured as websites.

Alias records work like CNAME record in that you can map one DNS name (`www.example.com`) to another `target` DNS name (`elb1234.elb.amazonaws.com`)

**Key Difference** : A CNAME can't be used for naked domain names (zone apex record.) You can't have a CNAME for `http://acloud.guru`, it must be either an A record or an Alias.



### Exam Tips

* ELBs do not have pre-defined IPv4 addresses; you resolve to them using a DNS name.
* Understand the difference between an Alias Record and a CNAME.
* Given the choice, always choose an Alias Record over a CNAME.

#### COMMIN DNS TYPES

* SOA Records
* NS Recods
* A Records
* CNAMES
* MX Records
* PTR Records



## 52. Register A Domain Name

### Exam Tips

* You can buy domain names directly with AWS.
* It can take up to 3 days to register depending on the circumstances.



## 53. Route53 Routing Policies Available on AWS.

### The Following Routing Policies Are Available With Route53;

* Simple Routing
* Weighted Routing 
* Latency-Based Routing 
* Failover Routing 
* Geolocation Routing 
* Geoproximity Routing (Traffic Flow only)
* Multivalue Answer Routing 



## 54 ~ 59. 

### Simple Routing Policy

If you choose the simple routing policy you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route53 returns all values to the user in a random order.

![스크린샷 2019-12-20 오후 4.30.05](img/스크린샷 2019-12-20 오후 4.30.05.png)

> Route53 just picks these in random orders.



### Weighted Routing Policy

Allows you split your traffic based on different weights assigned.

For example, you can set 10% of your traffic to go to US-EAST-1 and 90% to go to EU-WEST-1.

![스크린샷 2019-12-20 오후 4.34.14](img/스크린샷 2019-12-20 오후 4.34.14.png)

#### Health Checks

* You can set health checks on individual record sets.
* If a record set fails a health check it will be removed from Route53 until it passes the health check.
* You can set SNS notifications to alert you if a health check is failed.



### Latency-Based Policy

Allows you to route your traffic based on the lowest network latency for your end user (ie which region will give them the fast response time). 

To use latency-based routing, you create a latency resource record set fro the Amazon EC2 (or ELB) resource in each region that hosts your website. When Amazon Route 53 recerives a query for your site, it selects the latency resource record set for the region that gives the user the lowest latency. Route53 then responds with the value associated with that resourcerecord set.

![스크린샷 2019-12-20 오후 4.45.56](img/스크린샷 2019-12-20 오후 4.45.56.png)

> 강의에서 VPN 으로 다른 서버들을 접근하는 것을 보여줌.



### Failover Routing Policy

Failover routing policies are used when you want to create an active/passive setup. For example, you may wnat your primary site to be in EU-WEST-2 and your secondary DR Site in AP-SOUTHEAST-2.

Roue53 will monitor the health of your primary site using a health check.

A health check monitors the health of your end points.

![스크린샷 2019-12-20 오후 4.50.40](img/스크린샷 2019-12-20 오후 4.50.40.png)



### Geolocation Routing Poilicy

Geolocation routing lets you choose where your traffic will be sent based on the geographic location of your users (ie the location from which DNS queries originate). For example, you might want all queires from Europe to be routed to a fleet of EC2 instances that are specifically configured for your European customers. These servers may have the local language of your European customers and all prices are displayed in Euros.

![스크린샷 2019-12-20 오후 4.53.30](img/스크린샷 2019-12-20 오후 4.53.30.png)

> In this example, Route53 will send the European customers to EU-WEST-1 and the US customers to US-EAST-1.



### Geoproximity Routing Poilicy (Traffic Flow Only)

Geoproximity routing lets AMazon Route53 route traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic of less to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

**To use geoproximity routing you must use Route 53 traffic flow.**

![스크린샷 2019-12-20 오후 4.57.22](img/스크린샷 2019-12-20 오후 4.57.22.png)

### Multivalue Answer Policy

Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record, buy multivalue answer routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources.

**This is similar to simple routing however it allows you to put health checks on each record set.**

![스크린샷 2019-12-20 오후 5.39.47](img/스크린샷 2019-12-20 오후 5.39.47.png)

