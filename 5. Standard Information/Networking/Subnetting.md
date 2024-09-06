---
tags:
  - Networking
  - StandardInformation
---
A subnet is a logical segment of a network that uses IP addresses with the same network address. We can think of a subnet as a labelled entrance on a large building corridor. For example, this could be a glass door that separates various departments of a company building. With the help of subnetting, we can create a specific subnet by ourselves or find out the following outline of the respective network:

|**Details of**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**Decimal**|
|---|---|---|---|---|---|
|IPv4|`1100 0000`|`1010 1000`|`0000 1100`|`10`10 0000|192.168.12.160`/26`|
|Subnet mask|`1111 1111`|`1111 1111`|`1111 1111`|`11`00 0000|`255.255.255.192`|
|Bits|/8|/16|/24|/32|

## VLAN Memberships

Network administrators can assign the ports of a switch to `VLANs` either statically or dynamically. Static `VLAN` assignment, which is the simplest and most common method, involves assigning each port to a `VLAN` manually using the switch's `network operating system`; this must be done for all switches separately (it is essential to keep in mind that endpoints connecting to these ports are unaware of the existence of `VLANs`). In contrast, dynamic `VLAN` assignment automatically determines an endpoint's `VLAN` membership based on `MAC` addresses or protocols. The system administrator can register the `MAC` addresses in a centralized `VLAN` management service/database, such as the `VLAN Membership Policy Server` (`VMPS`) service, and then the switch queries the database of `VMPS` to determine the `VLAN` of the endpoint with that specific `MAC` address. Regardless of their flexibility and mobility, dynamic `VLANs` increase administrative overhead.

Security-wise, static `VLANs` are the more secure option because a port will forever be tied to a specific `VLAN` ID, unless changed manually afterward. For dynamic `VLANs`, an attacker could potentially utilize tools such as [macchanger](https://github.com/alobbs/macchanger) to spoof the MAC address of legitimate endpoints and attain membership of their `VLANs`, therefore sniffing all network traffic sent through them.

## Access and Trunk Ports

Any port on a `VLAN`-enabled switch must be either an `access port` or a `trunk port`. `Access ports` belong to and can carry the traffic of only one `VLAN` (or in some cases two, with the second being for `voice traffic`); any traffic arriving on an `access port` is assumed to belong to the `VLAN` the port was assigned. On the other hand, `trunk ports` can carry multiple `VLANs` at the same time; `trunk links` connect two `trunk ports` on two switches (or a switch and router) to allow information from multiple `VLANs` to be carried out across switches.

## VLAN Identification

Standard `802.3` `Ethernet` frames do not contain `VLAN` information; therefore, switches and other `VLAN`-enabled devices need a mechanism to keep track of all the `VLAN` information associated with a packet while traversing `VLAN`-enabled devices. Two main `trunking methods` are utilized to achieve this, `ISL` and `IEEE 802.1Q`.

#### Inter-Switch Link (ISL)

`Inter-Switch Link` (`ISL`) is a Cisco-proprietary protocol used for trunking between `VLAN`-enabled devices. Although `ISL` is one of the first `trunking methods` (predating `802.1Q`), it is deprecated and not as widely used in modern Cisco switches (and routers). Instead, most only support the widely adopted `802.1Q`. `ISL` encapsulated the entire `Ethernet` frame, including the original `Ethernet` header and the `VLAN` tag, adding its 26-byte header and 4-byte trailer.

#### IEEE 802.1Q

To ensure interoperability of `VLAN` technologies from the various network-equipments vendors, the `Institute of Electrical and Electronics Engineers` (`IEEE`) developed the [802.1Q](https://ieeexplore.ieee.org/document/10004498) specification in 1998. The `IEEE 802` committee had to change the `802.3` `Ethernet` frame format by adding a pair of 2-byte fields, `TPID` and `TCI` (which consists of three subfields, `PCP`, `DEI`, and `VID`), resulting in a `VLAN`-compliant `802.1Q` `Ethernet` frame.

![8023_Legacy_8021Q_Ethernet_Frames.png](https://academy.hackthebox.com/storage/modules/34/8023_Legacy_8021Q_Ethernet_Frames.png)

`Tag protocol identifier` (`TPID`) is a 16-bit field always set to `0x8100` to identify the `Ethernet` frame as an `802.1Q`-tagged frame. `Tag Control Information` (`TCI`) is a 16-bit field containing `Priority code point` (`PCP`), `Drop eligible indicator` (`DEI`) (previously known as `Canonical format indicator` (`CFI`)), and `VLAN identifier` (`VID`). The main field concerning `VLANs` is `VID`, occupying the low-order 12-bits of `TCI`. Since it is 12 bits, it allows 2^12 - 2 = 4096 (remember, `0` and `4095` are reserved) `VLAN` IDs. Therefore, an `802.1Q`-tagged frame can contain information for 4094 `VLANs`; the practice of inserting multiple `802.1Q` tags within a single packet is known as `Double Tagging`, introduced by [802.1ad](https://standards.ieee.org/ieee/802.1Q/10323/). `VLAN tagging` is the process of inserting `VLAN` information into an `802.1Q` `Ethernet header`, while `VLAN untagging` is the process of removing the `VLAN` information from an `802.1Q`-tagged `Ethernet` frame and forwarding the packet to the destined ports.