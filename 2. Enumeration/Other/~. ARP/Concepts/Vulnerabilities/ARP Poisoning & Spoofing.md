---
tags:
  - Enumeration
  - Misc
  - ARP
  - Concepts
  - Vulnerabilities
---
ARP poisoning, also known as ARP spoofing, is a type of cyber attack where an attacker sends falsified Address Resolution Protocol (ARP) messages over a local area network. This results in linking the attacker's MAC address with the IP address of a legitimate network device or server. 

This allows the attacker to intercept, modify, or block traffic between two communicating devices on the same network.


| **Step** | **Description**                                                                                                                                                                                                                                           |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `1`      | Consider a network with three machines: the victim's computer, the router, and the attacker's machine.                                                                                                                                                    |
| `2`      | The attacker initiates their ARP cache poisoning scheme by dispatching counterfeit ARP messages to both the victim's computer and the router.                                                                                                             |
| `3`      | The message to the victim's computer asserts that the gateway's (router's) IP address corresponds to the physical address of the attacker's machine.                                                                                                      |
| `4`      | Conversely, the message to the router claims that the IP address of the victim's machine maps to the physical address of the attacker's machine.                                                                                                          |
| `5`      | On successfully executing these requests, the attacker may manage to corrupt the ARP cache on both the victim's machine and the router, causing all data to be misdirected to the attacker's machine.                                                     |
| `6`      | If the attacker configures traffic forwarding, they can escalate the situation from a denial-of-service to a man-in-the-middle attack.                                                                                                                    |
| `7`      | By examining other layers of our network model, we might discover additional attacks. The attacker could conduct DNS spoofing to redirect web requests to a bogus site or perform SSL stripping to attempt the interception of sensitive data in transit. |

## Mitigations 

1. `Static ARP Entries`: By disallowing easy rewrites and poisoning of the ARP cache, we can stymie these attacks. This, however, necessitates increased maintenance and oversight in our network environment.
2. `Switch and Router Port Security`: Implementing network profile controls and other measures can ensure that only authorized devices can connect to specific ports on our network devices, effectively blocking machines attempting ARP spoofing/poisoning.

## Detecting ARP Spoofing 

A key red flag we need to monitor is any anomaly in traffic emanating from a specific host. For instance, one host incessantly broadcasting ARP requests and replies to another host could be a tell-tale sign of ARP spoofing.

Multiple [[IP Addresses]] mapped to one [[MAC Addresses]].

[[Wireshark]] filter to detect ARP spoofing: 

```
arp.duplicate-address-detected && arp.opcode == 2
```