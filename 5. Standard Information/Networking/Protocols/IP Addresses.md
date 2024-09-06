---
tags:
  - Networking
  - Protocols
  - StandardInformation
---

[IP Protocol](https://tools.ietf.org/html/rfc791)
# IPv4

The most common method of assigning IP addresses is `IPv4`, which consists of a `32`-bit binary number combined into `4 bytes` consisting of `8`-bit groups (`octets`) ranging from `0-255`. These are converted into more easily readable decimal numbers, separated by dots and represented as dotted-decimal notation.

Thus an IPv4 address can look like this:

| **Notation** | **Presentation**                        |
| ------------ | --------------------------------------- |
| Binary       | 0111 1111.0000 0000.0000 0000.0000 0001 |
| Decimal      | 127.0.0.1                               |
# Classes

|**`Class`**|**Network Address**|**First Address**|**Last Address**|**Subnetmask**|**CIDR**|**Subnets**|**IPs**|
|---|---|---|---|---|---|---|---|
|`A`|1.0.0.0|1.0.0.1|127.255.255.255|255.0.0.0|/8|127|16,777,214 + 2|
|`B`|128.0.0.0|128.0.0.1|191.255.255.255|255.255.0.0|/16|16,384|65,534 + 2|
|`C`|192.0.0.0|192.0.0.1|223.255.255.255|255.255.255.0|/24|2,097,152|254 + 2|
|`D`|224.0.0.0|224.0.0.1|239.255.255.255|Multicast|Multicast|Multicast|Multicast|
|`E`|240.0.0.0|240.0.0.1|255.255.255.255|reserved|reserved|reserved|reserved|


## CIDR

`Classless Inter-Domain Routing` (`CIDR`) is a method of representation and replaces the fixed assignment between IPv4 address and network classes (A, B, C, D, E). The division is based on the subnet mask or the so-called `CIDR suffix`, which allows the bitwise division of the IPv4 address space and thus into `subnets` of any size. The `CIDR suffix` indicates how many bits from the beginning of the IPv4 address belong to the network. It is a notation that represents the `subnet mask` by specifying the number of `1`-bits in the subnet mask.

---
# IPv6 Addresses

`IPv6` is the successor of IPv4. In contrast to IPv4, the `IPv6` address is `128` bit long. The `prefix` identifies the host and network parts. The Internet Assigned Numbers Authority (`IANA`) is responsible for assigning IPv4 and IPv6 addresses and their associated network portions. In the long term, `IPv6` is expected to completely replace IPv4, which is still predominantly used on the Internet. In principle, however, IPv4 and IPv6 can be made available simultaneously (`Dual Stack`).

`IPv6` is a protocol with many new features, which also has many other advantages over IPv4:

- Larger address space
- Address self-configuration (SLAAC)
- Multiple IPv6 addresses per interface
- Faster routing
- End-to-end encryption (IPsec)
- Data packages up to 4 GByte

|**Features**|**IPv4**|**IPv6**|
|---|---|---|
|Bit length|32-bit|128 bit|
|OSI layer|Network Layer|Network Layer|
|Adressing range|~ 4.3 billion|~ 340 undecillion|
|Representation|Binary|Hexadecimal|
|Prefix notation|10.10.10.0/24|fe80::dd80:b1a9:6687:2d3b/64|
|Dynamic addressing|DHCP|SLAAC / DHCPv6|
|IPsec|Optional|Mandatory|
There are four different types of IPv6 addresses:

|**Type**|**Description**|
|---|---|
|`Unicast`|Addresses for a single interface.|
|`Anycast`|Addresses for multiple interfaces, where only one of them receives the packet.|
|`Multicast`|Addresses for multiple interfaces, where all receive the same packet.|
|`Broadcast`|Do not exist and is realized with multicast addresses.|