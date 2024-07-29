[How Amazon VPC Works](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)
[What Is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)

A virtual private cloud (VPC) is an isolated network that you create in the AWS Cloud, similar to a traditional network in a data centre. When you create an Amazon VPC, you must choose three main factors:

- Name of the VPC
- Region where the VPC will live – A VPC spans all the Availability Zones within the selected Region.
- IP range for the VPC in CIDR notation


![[Pasted image 20240729154031.png]]

## Creating a subnet  

After you create your VPC, you must create subnets inside the network. In AWS, subnets are used to provide high availability and connectivity options for your resources. Use a public subnet for resources that must be connected to the internet and a private subnet for resources that won't be connected to the internet.

![[Pasted image 20240729154057.png]]

When you create your subnets, keep high availability in mind. To maintain redundancy and fault tolerance, create at least two subnets configured in two Availability Zones.

![[Pasted image 20240729154315.png]]

## Gateways

### Internet gateway  

To activate internet connectivity for your VPC, you must create an internet gateway. Think of the gateway as similar to a modem. Just as a modem connects your computer to the internet, the internet gateway connects your VPC to the internet. Unlike your modem at home, which sometimes goes down or offline, an internet gateway is highly available and scalable. After you create an internet gateway, you attach it to your VPC.

![[Pasted image 20240729154357.png]]


### Virtual private gateway  

[How AWS Site-to-Site VPN Works](https://docs.aws.amazon.com/vpn/latest/s2svpn/how_it_works.html)

A virtual private gateway connects your VPC to another private network. When you create and attach a virtual private gateway to a VPC, the gateway acts as anchor on the AWS side of the connection. On the other side of the connection, you will need to connect a customer gateway to the other private network. A customer gateway device is a physical device or software application on your side of the connection. When you have both gateways, you can then establish an encrypted virtual private network (VPN) connection between the two sides.

![[Pasted image 20240729154438.jpg]]

