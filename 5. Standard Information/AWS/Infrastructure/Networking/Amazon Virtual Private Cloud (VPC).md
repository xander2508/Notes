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

# Routing

[Configure Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)

Nothing comes into a VPC or out of a VPC without explicit setting it through gateways or routing.

A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. AWS assumes that when you create a new VPC with subnets, you want traffic to flow between them. Therefore, the default configuration of the main route table is to allow traffic between all subnets in the local network. The following rules apply to the main route table:

- You cannot delete the main route table.
- You cannot set a gateway route table as the main route table.
- You can replace the main route table with a custom subnet route table.
- You can add, remove, and modify routes in the main route table.
- You can explicitly associate a subnet with the main route table, even if it's already implicitly associated.

The main route table is used implicitly by subnets that do not have an explicit route table association. However, you might want to provide different routes on a per-subnet basis for traffic to access resources outside of the VPC.

Each custom route table that you create will have the local route already inside it, allowing communication to flow between all resources and subnets inside the VPC. You can protect your VPC by explicitly associating each new subnet with a custom route table and leaving the main route table in its original default state.


# Security

A network access control list (ACL) lets you control what kind of traffic is allowed to enter or leave your subnet. You can configure this by setting up rules that define what you want to filter.

![[Pasted image 20240729160924.png]]

## Default network ACL

Allows all traffic in and out of the subnet.

| Inbound    |                  |              |                |            |                   |
| ---------- | ---------------- | ------------ | -------------- | ---------- | ----------------- |
| **Rule #** | **Type**         | **Protocol** | **Port Range** | **Source** | **Allow or Deny** |
| 100        | All IPv4 traffic | All          | All            | 0.0.0.0/0  | ALLOW             |
| *          | All IPv4 traffic | All          | All            | 0.0.0.0/0  | DENY              |

| **Outbound** |                  |              |                |                 |                   |
| ------------ | ---------------- | ------------ | -------------- | --------------- | ----------------- |
| **Rule #**   | **Type**         | **Protocol** | **Port Range** | **Destination** | **Allow or Deny** |
| 100          | All IPv4 traffic | All          | All            | 0.0.0.0/0       | ALLOW             |
| *            | All IPv4 traffic | All          | All            | 0.0.0.0/0       | DENY              |
## Custom network ACL

| **Inbound** |                  |              |          |                   |                                                                                                                            |
| ----------- | ---------------- | ------------ | -------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Rule #**  | **Source IP**    | **Protocol** | **Port** | **Allow or Deny** | **Comments**                                                                                                               |
| 100         | All IPv4 traffic | TCP          | 443      | ALLOW             | Allows inbound HTTPS traffic from anywhere                                                                                 |
| 130         | 192.0.2.0/24     | TCP          | 3389     | ALLOW             | Allows inbound RDP traffic to the web servers from your home network’s public IP address range (over the internet gateway) |
| *           | All IPv4 traffic | All          | All      | DENY              | Denies all inbound traffic not already handled by a preceding rule (not modifiable)                                        |

| **Outbound** |                    |              |            |                   |                                                                                                              |
| ------------ | ------------------ | ------------ | ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------ |
| **Rule #**   | **Destination IP** | **Protocol** | **Port**   | **Allow or Deny** | **Comments**                                                                                                 |
| 120          | 0.0.0.0/0          | TCP          | 1025-65535 | ALLOW             | Allows outbound responses to clients on the internet (serving people visiting the web servers in the subnet) |
| *            | 0.0.0.0/0          | All          | All        | DENY              | Denies all outbound traffic not already handled by a preceding rule (not modifiable)                         |
