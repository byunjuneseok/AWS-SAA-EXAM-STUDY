# QUIZ

Q1. 



2. Route 53 is Amazon's DNS Service.

- **TRUE**
- FALSE



3. Route 53 is named so because ________.

- It was invented in 1953.
- Route 66 was already registered with Microsoft.
- **The DNS Port is on Port 53 and Route 53 is a DNS Service.**
- Beats me – only people in marketing can tell you the reason behind its name.



4. You have created a new subdomain for your popular website, and you need this subdomain to point to an Elastic Load Balancer using Route53. Which DNS record set should you create?

- A
- AAAA
- MX
- CNAME



5. True or False: There is a limit to the number of domain names that you can manage using Route 53.

- True. There is a hard limit of 10 domain names. You cannot go above this number.
- **True and False. With Route 53, there is a default limit of 50 domain names. However, this limit can be increased by contacting AWS support.**
- False. By default, you can support as many domain names on Route 53 as you want.



6. You are hosting a website and would like visitors from United Kingdom to see a different site than those in Australia. Which Routing Policy would help you to accomplish this?

- Failover routing policy
- **Geolocation routing policy**
- Geoproximity routing policy
- Latency routing policy





7. Your company hosts 10 web servers all serving the same web content in AWS. They want Route 53 to serve traffic to random web servers. Which routing policy will meet this requirement, and provide the best resiliency?

- Simple Routing
- Weighted Routing
- **Multivalue Routing**
- Latency Routing

> Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. Route 53 responds to DNS queries with up to eight healthy records and gives different answers to different DNS resolvers. The choice of which to use is left to the requesting service effectively creating a form or randomization.