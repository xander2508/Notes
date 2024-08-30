---
tags:
  - Architecture
---
Although containers are often referred to as a new technology, the idea started in the 1970s with certain UNIX kernels (the central core of the operating system) having the ability to separate their processes through isolation. At the time, this was configured manually, making operations complex.  
  
With the evolution of the open-source software community, containers evolved. Today, containers are used as a solution to problems of traditional compute, including the issue of getting software to run reliably when it moves from one compute environment to another.

A container is a standardized unit that packages your code and its dependencies. This package is designed to run reliably on any platform, because the container creates its own independent environment. With containers, workloads can be carried from one place to another, such as from development to production or from on-premises environments to the cloud.

An example of a containerization platform is [[Docker]]. Docker is a popular container runtime that simplifies the management of the entire operating system stack required for container isolation, including networking and storage. Docker helps customers create, package, deploy, and run containers.

## Difference between VMs and containers

![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1722265200/iWP68hjrw6q_ADNOlBS5Ag/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/1iikq77Axc3_R0px_aLZuLt2uEP1sRZeR.png)

Compared to virtual machines (VMs), containers share the same operating system and kernel as the host that they are deployed on.

Containers share the same operating system and kernel as the host that they exist on. But virtual machines contain their own operating system. Each virtual machine must maintain a copy of an operating system, which results in a degree of wasted resources.  
  
A container is more lightweight. Containers spin up quicker, almost instantly. This difference in startup time becomes instrumental when designing applications that must scale quickly during I/O bursts.

Containers can provide speed, but virtual machines offer the full strength of an operating system and more resources, like package installation, dedicated kernel, and more.