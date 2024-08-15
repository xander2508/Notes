
# Microservices

Microservices are an architectural and organizational approach to software development where software is composed of small independent services that communicate over well-defined APIs. These services are owned by small, self-contained teams.

We can think of microservices as independent components of the web application, which in most cases are programmed for one task only

Microservices architectures make applications easier to scale and faster to develop, enabling innovation and accelerating time-to-market for new features.

The communication between these microservices is `stateless`, which means that the request and response are independent. This is because the stored data is `stored separately` from the respective microservices.

[microservices-on-aws.pdf](https://d1.awsstatic.com/whitepapers/microservices-on-aws.pdf)
![[Pasted image 20240514191950.png]]

# Serverless 

A serverless architecture is a way to build and run applications and services without having to manage infrastructure. Your application still runs on servers, but all the server management is done by AWS. You no longer have to provision, scale, and maintain servers to run your applications, databases, and storage systems. Learn more about serverless computing [here](https://aws.amazon.com/serverless/).


# Backend Server Architecture 

| Combinations                                                      | Components                                         |
| ----------------------------------------------------------------- | -------------------------------------------------- |
| [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle))      | `Linux`, `Apache`, `MySQL`, and `PHP`.             |
| [WAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle)#WAMP) | `Windows`, `Apache`, `MySQL`, and `PHP`.           |
| [WINS](https://en.wikipedia.org/wiki/Solution_stack)              | `Windows`, `IIS`, `.NET`, and `SQL Server`         |
| [MAMP](https://en.wikipedia.org/wiki/MAMP)                        | `macOS`, `Apache`, `MySQL`, and `PHP`.             |
| [XAMPP](https://en.wikipedia.org/wiki/XAMPP)                      | Cross-Platform, `Apache`, `MySQL`, and `PHP/PERL`. |