---
tags:
  - AWS
  - AmazonWebServices
  - Services
  - Compute
  - ContainerServices
  - StandardInformation
---

[Containers on AWS](https://aws.amazon.com/containers/services/)
[Amazon Elastic Container Service (Amazon ECS)](https://aws.amazon.com/ecs/)
[GitHub: Amazon ECS Agent](https://github.com/aws/amazon-ecs-agent)
[Amazon ECS Container Instances](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_instances.html)
[Coursera course: Building Containerized Applications on AWS](https://www.coursera.org/learn/containerized-apps-on-aws)


Amazon ECS is an end-to-end container orchestration service that helps you spin up new containers. With Amazon ECS, your containers are defined in a task definition that you use to run an individual task or a task within a service. You have the option to run your tasks and services on 
a serverless infrastructure that's managed by another AWS service called [[AWS Fargate]]. 

Alternatively, for more control over your infrastructure, you can run your tasks and services on a cluster of EC2 instances that you manage.

![[Pasted image 20240729141540.png]]

If you choose to have more control by running and managing your containers on a cluster of Amazon EC2 instances, you will also need to install the Amazon ECS container agent on your EC2 instances. Note that an EC2 instance with the container agent installed is often called a container instance. This container agent is open source and responsible for communicating to the Amazon ECS service about cluster management details. You can run the agent on both Linux and Windows AMIs. 

![An EC2 instance with the container agent installed is called a container instance.](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1722265200/iWP68hjrw6q_ADNOlBS5Ag/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/XbD8apMKo5wCAHO6_YiX8p1udFI_1rzlu.jpg)

When the Amazon ECS container instances are up and running, you can perform actions that include, but are not limited to, the following:

- Launching and stopping containers
- Getting cluster state
- Scaling in and out
- Scheduling the placement of containers across your cluster
- Assigning permissions
- Meeting availability requirements

## Tasks

To prepare your application to run on Amazon ECS, you create a task definition. The task definition is a text file, in JSON format, that describes one or more containers. A task definition is similar to a blueprint that describes the resources that you need to run a container, such as CPU, memory, ports, images, storage, and networking information.  
  
Here is a simple task definition that you can use for your corporate directory application. In this example, this runs on the Nginx web server.

```json
{
	"family": "webserver",
	"containerDefinitions": [ {
		"name": "web",
		"image": "nginx",
		"memory": "100",
		"cpu": "99"
	} ],
	"requiresCompatibilities": [ "FARGATE" ],
	"networkMode": "awsvpc",
	"memory": "512",
	"cpu": "256"
}
```