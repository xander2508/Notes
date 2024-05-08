
The device must also be configured with the correct network settings, such as the network name / [Service Set Identifier](https://www.geeksforgeeks.org/service-set-identifier-ssid-in-computer-network/) (`SSID`) and `password`. So, to connect to the router, the laptop uses a wireless networking protocol called [IEEE 802.11](https://en.wikipedia.org/wiki/IEEE_802.11). This protocol defines the technical details of how wireless devices communicate with each other and with WAPs. When a device wants to join a WiFi network, it sends a request to the WAP to initiate the connection process. This request is known as a `connection request frame` or `association request` and is sent using the `IEEE 802.11` wireless networking protocol. The connection request frame contains various fields of information, including the following but not limited to:

|                                |                                                                                              |
| ------------------------------ | -------------------------------------------------------------------------------------------- |
| `MAC address`                  | A unique identifier for the device's wireless adapter.                                       |
| `SSID`                         | The network name, also known as the `Service Set Identifier` of the WiFi network.            |
| `Supported data rates`         | A list of the data rates the device can communicate.                                         |
| `Supported channels`           | A list of the `channels` (frequencies) on which the device can communicate.                  |
| `Supported security protocols` | A list of the security protocols that the device is capable of using, such as `WPA2`/`WPA3`. |

The device then uses this information to configure its wireless adapter and connect to the WAP. Once the connection is established, the device can communicate with the WAP and other network devices. It can also access the Internet and other online resources through the WAP, which acts as a gateway to the wired network. However, the `SSID` can be hidden by disabling broadcasting. That means that devices that search for that specific WAP will not be able to identify its `SSID`. Nevertheless, the `SSID` can still be found in the authentication packet.

In addition to the `IEEE 802.11` protocol, other networking protocols and technologies may also be used, like TCP/IP, DHCP, and WPA2, in a WiFi network to perform tasks such as assigning IP addresses to devices, routing traffic between devices, and providing security.

#### WEP Challenge-Response Handshake

The challenge-response handshake is a process to establish a secure connection between a WAP and a client device in a wireless network that uses the WEP security protocol. This involves exchanging packets between the WAP and the client device to authenticate the device and establish a secure connection.

|**Step**|**Who**|**Description**|
|---|---|---|
|1|`Client`|Sends an association request packet to the WAP, requesting access.|
|2|`WAP`|Responds with an association response packet to the client, which includes a challenge string.|
|3|`Client`|Calculates a response to the challenge string and a shared secret key and sends it back to the WAP.|
|4|`WAP`|Calculates the expected response to the challenge with the same shared secret key and sends an authentication response packet to the client.|
## Security Features

WiFi networks have several security features to protect against unauthorized access and ensure the privacy and integrity of data transmitted over the network. Some of the leading security features include but are not limited to:

- Encryption
- Access Control
- Firewall

#### Encryption

We can use various encryption algorithms to protect the confidentiality of data transmitted over wireless networks. The most common encryption algorithms in WiFi networks are [Wired Equivalent Privacy](https://en.wikipedia.org/wiki/Wired_Equivalent_Privacy) (`WEP`), [WiFi Protected Access 2](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access#WPA2) (`WPA2`), and [WiFi Protected Access 3](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access#WPA3) (`WPA3`).

#### Access Control

WiFi networks are configured by default to allow authorized devices to join the network using specific authentication methods. However, these methods can be changed by requiring a password or a unique identifier (such as a MAC address) to identify authorized devices.

#### Firewall

A firewall is a security system that controls incoming and outgoing network traffic based on predetermined security rules. For example, WiFi routers often have built-in firewalls that can block incoming traffic from the Internet and protect against various types of cyber threats.

 ------------------------------ 
# WEP

`WEP` uses a `40-bit` or `104-bit` key to encrypt data, while `WPA using AES` uses a `128-bit` key. Longer keys provide more robust encryption and are more resistant to attacks. However, it is vulnerable to various attacks that can allow an attacker to decrypt data transmitted over the network. In addition, WEP is not compatible with newer devices and operating systems and is generally no longer considered secure. Finally, `WEP` uses the `RC4 cipher` encryption algorithm, which makes it vulnerable to attacks.

However, WEP uses a `shared key` for authentication, which means the same key is used for encryption and authentication. There are two versions of the WEP protocol:

- `WEP-40`/`WEP-64`
- `WEP-104`

`WEP-40`, also known as `WEP-64`, uses a `40-bit` (secret) key, while `WEP-104` uses a `104-bit` key. The key is divided into an [Initialization Vector](https://en.wikipedia.org/wiki/Initialization_vector) (`IV`) and a `secret key`.

The `IV` is a small value included in the packet header along with the encrypted data and is used to create the key for both `WEP-40` and `WEP-104` and is included to ensure that each key is unique. The secret key is a series of random bits used to encrypt the data. However, the `WEP-104` has a `80-bits` long `secret key`. Let us look at the following table to see the differences clearly:

|**Protocol**|**IV**|**Secret Key**|
|---|---|---|
|`WEP-40`/`WEP-64`|24-bit|40-bit|
|`WEP-104`|24-bit|80-bit|

However, since the IV in WEP is relatively small, we can brute force it, try every possible combination of characters for it, and determine the correct value. Afterward, we can use it to decrypt the data in the packet. This allows us to access the data transmitted over the wireless network and potentially compromise the network's security.

#### WPA

`WPA` provides the highest level of security and is not susceptible to the same types of attacks as WEP. In addition, WPA uses more secure authentication methods, such as a [Pre-Shared Key](https://en.wikipedia.org/wiki/Pre-shared_key) (`PSK`) or an 802.1X authentication server, which provide stronger protection against unauthorized access. Although older devices may not support WPA is compatible with most devices and operating systems. All wireless networks, especially in critical infrastructure like offices, should generally implement at least `WPA2` or even `WPA3` encryption.

---
## Authentication Protocols

[Lightweight Extensible Authentication Protocol](https://en.wikipedia.org/wiki/Lightweight_Extensible_Authentication_Protocol) (`LEAP`) and [Protected Extensible Authentication Protocol](https://en.wikipedia.org/wiki/Protected_Extensible_Authentication_Protocol) (`PEAP`) are authentication protocols used to secure wireless networks to provide a secure method for authenticating devices on a wireless network and are often used in conjunction with WEP or WPA to provide an additional layer of security.

LEAP and PEAP are both based on the [Extensible Authentication Protocol](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol) (`EAP`), a framework for authentication used in various networking contexts. However, one key difference between `LEAP` and `PEAP` is how they secure the authentication process.

- `LEAP` uses a `shared key` for authentication, which means that the `same key` is used for `encryption and authentication`.

This can make it relatively easy for us to gain access to the network if the key is compromised.

However, `PEAP` uses a more secure authentication method called tunneled [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (`TLS`). This method establishes a secure connection between the device and the WAP using a `digital certificate`, and an encrypted tunnel protects the authentication process. This provides more robust protection against unauthorized access and is more resistant to attacks.

---

## TACACS+

In a wireless network, when a wireless access point (WAP) sends an authentication request to a [Terminal Access Controller Access-Control System Plus](https://www.ciscopress.com/articles/article.asp?p=422947&seqNum=4) (`TACACS+`) server, it is likely that the `entire request packet` will be encrypted to protect the confidentiality and integrity of the request.

`TACACS+` is a protocol used to authenticate and authorize users accessing network devices, such as routers and switches. When a WAP sends an authentication request to a `TACACS+` server, the request typically includes the user's credentials and other information about the session.

Encrypting the authentication request helps to ensure that this sensitive information is not visible to unauthorized parties who may be able to intercept the request. At the same time, it is being transmitted over the network. It also helps prevent tampering with the request or replacing it with a malicious request of their own.

Several encryption methods may be used to encrypt the authentication request, such as `SSL`/`TLS` or `IPSec`. The specific encryption me