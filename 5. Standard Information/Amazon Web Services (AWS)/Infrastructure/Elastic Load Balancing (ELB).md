---
tags:
  - AWS
  - AmazonWebServices
  - Infrastructure
---

[Elastic Load Balancing features](https://aws.amazon.com/elasticloadbalancing/features/#Product_comparisons)

You can use a load balancer to distribute the requests across all the servers hosting the application. To do this, the load balancer needs to take all the traffic and redirect it to the backend servers based on an algorithm. The most popular algorithm is round robin, which sends the traffic to each server one after the other.

![[Pasted image 20240730151125.png]]

## ELB features

The ELB service provides a major advantage over using your own solution to do load balancing. Mainly, you don’t need to manage or operate ELB. It can distribute incoming application traffic across EC2 instances, containers, IP addresses, and Lambda functions. Other key features include the following:

- Hybrid mode – Because ELB can load balance to IP addresses, it can work in a hybrid mode, which means it also load balances to on-premises servers.
- High availability – ELB is highly available. The only option you must ensure is that the load balancer's targets are deployed across multiple Availability Zones.
- Scalability– In terms of scalability, ELB automatically scales to meet the demand of the incoming traffic. It handles the incoming traffic and sends it to your backend application.


## Health checks

Monitoring is an important part of load balancers because they should route traffic to only healthy EC2 instances. That’s why ELB supports two types of health checks as follows:

- Establishing a connection to a backend EC2 instance using TCP and marking the instance as available if the connection is successful.
- Making an HTTP or HTTPS request to a webpage that you specify and validating that an HTTP response code is returned.

After determining the availability of a new EC2 instance, the load balancer starts sending traffic to it. If ELB determines that an EC2 instance is no longer working, it stops sending traffic to it and informs [[Amazon EC2 Auto Scaling]]. It is the responsibility of Amazon EC2 Auto Scaling to remove that instance from the group and replace it with a new EC2 instance. Traffic is only sent to the new instance if it passes the health check.


## ELB components

The ELB service is made up of three main components: rules, listeners, and target groups.

The client connects to the listener. This is often called client side. To define a listener, a port must be provided in addition to the protocol, depending on the load balancer type. There can be many listeners for a single load balancer.

To associate a target group to a listener, you must use a rule. Rules are made up of two conditions. The first condition is the source IP address of the client. The second condition decides which target group to send the traffic to.

The backend servers, or server side, are defined in one or more target groups. This is where you define the type of backend you want to direct traffic to, such as EC2 instances, Lambda functions, or IP addresses. Also, a health check must be defined for each target group.


## Types of load balancers

We will cover three types of load balancers: Application Load Balancer (ALB), Network Load Balancer (NLB), and Gateway Load Balancer (GLB).

### Application Load Balancer

[How AWS WAF works](https://docs.aws.amazon.com/waf/latest/developerguide/how-aws-waf-works.html)

An Application Load Balancer functions at Layer 7 of the Open Systems Interconnection (OSI) model. It is ideal for load balancing HTTP and HTTPS traffic. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply. It then routes traffic to targets based on the request content.

An Application Load Balancer can reply directly to the client with a fixed response, such as a custom HTML page. It can also send a redirect to the client. This is useful when you must redirect to a specific website or redirect a request from HTTP to HTTPS. It removes that work from your backend servers. [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/)

[Authenticate users using an Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/listener-authenticate-users.html)

An Application Load Balancer can authenticate users before they can pass through the load balancer. The Application Load Balancer uses the OpenID Connect (OIDC) protocol and integrates with other AWS services to support protocols, such as the following:

- SAML
- Lightweight Directory Access Protocol (LDAP)
- Microsoft Active Directory
- Others

 To pass HTTPS traffic through an Application Load Balancer, an SSL certificate is provided one of the following ways:
- Importing a certificate by way of IAM or ACM services
- Creating a certificate for free using ACM

If requests must be sent to the same backend server because the application is stateful, use the sticky session feature. This feature uses an HTTP cookie to remember which server to send the traffic to across connections.

### Network Load Balancer
  
A Network Load Balancer is ideal for load balancing TCP and UDP traffic. It functions at Layer 4 of the OSI model, routing connections from a target in the target group based on IP protocol data.

Routes requests from the same client to the same target.
Offers low latency for latency-sensitive applications.
Preserves the client-side source IP address.
Automatically provides a static IP address per Availability Zone (subnet).
Lets users assign a custom, fixed IP address per Availability Zone (subnet).
Uses Amazon Route 53 to direct traffic to load balancer nodes in other zones.

### Gateway Load Balancer

A Gateway Load Balancer helps you to deploy, scale, and manage your third-party appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. It provides a gateway for distributing traffic across multiple virtual appliances while scaling them up and down based on demand.


|Feature|ALB|NLB|GLB|
|---|---|---|---|
|**Load Balancer Type**|Layer 7|Layer 4|Layer 3 gateway and Layer 4 load balancing|
|**Target Type**|IP, instance, Lambda|IP, instance, ALB|IP, instance|
|**Protocol Listeners**|HTTP, HTTPS|TCP, UDP, TLS|IP|
|**Static IP and Elastic IP Address**||Yes||
|**Preserve Source IP Address**|Yes|Yes|Yes|
|**Fixed Response**|Yes|||
|**User Authentication**|Yes|