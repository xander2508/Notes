---
tags:
  - Networking
  - StandardInformation
---
A `Virtual Private Network` (`VPN`) is a technology that allows a secure and encrypted connection between a private network and a remote device.

For a VPNs to connect multiple remote locations, such as branch offices, into a single private network, making it easier to manage and access network resources. However, several components and requirements are necessary for a VPN to work:

|**Requirement**|**Description**|
|---|---|
|`VPN Client`|This is installed on the remote device and is used to establish and maintain a VPN connection with the VPN server. For example, this could be an OpenVPN client.|
|`VPN Server`|This is a computer or network device responsible for accepting VPN connections from VPN clients and routing traffic between the VPN clients and the private network.|
|`Encryption`|VPN connections are encrypted using a variety of encryption algorithms and protocols, such as AES and IPsec, to secure the connection and protect the transmitted data.|
|`Authentication`|The VPN server and client must authenticate each other using a shared secret, certificate, or another authentication method to establish a secure connection.|

The VPN client and server use these ports to establish and maintain the VPN connection. At the TCP/IP layer, a VPN connection typically uses the [Encapsulating Security Payload](https://www.ibm.com/docs/en/i/7.4?topic=protocols-encapsulating-security-payload) (`ESP`) protocol to encrypt and authenticate the VPN traffic. This allows the VPN client and server to exchange data over the public internet securely.

OpenVPN can be customized and configured by editing the configuration file `/etc/openvpn/server.conf`

---

## IPsec

[Internet Protocol Security](https://www.cloudflare.com/learning/network-layer/what-is-ipsec/) (`IPsec`) is a network security protocol that provides encryption and authentication for internet communications. It is a powerful and widely-used security protocol that provides encryption and authentication for internet communications and works by encrypting the data payload of each IP packet and adding an `authentication header` (`AH`), which is used to verify the integrity and authenticity of the packet. IPsec uses a combination of two protocols to provide encryption and authentication:

1. [Authentication Header](https://www.ibm.com/docs/en/i/7.1?topic=protocols-authentication-header) (`AH`): This protocol provides integrity and authenticity for IP packets but does not provide encryption. It adds an authentication header to each IP packet, which contains a cryptographic checksum that can be used to verify that the packet has not been tampered with.
    
2. [Encapsulating Security Payload](https://www.ibm.com/docs/en/i/7.4?topic=protocols-encapsulating-security-payload) (`ESP`): This protocol provides encryption and optional authentication for IP packets. It encrypts the data payload of each IP packet and optionally adds an authentication header, similar to AH.
    

IPsec can be used in two modes.

|**Mode**|**Description**|
|---|---|
|`Transport Mode`|In this mode, IPsec encrypts and authenticates the data payload of each IP packet but does not encrypt the IP header. This is typically used to secure end-to-end communication between two hosts.|
|`Tunnel Mode`|With this mode, IPsec encrypts and authenticates the entire IP packet, including the IP header. This is typically used to create a VPN tunnel between two networks.|

For example, an administrator could place a firewall in between. In order to facilitate IPsec VPN traffic from a VPN client outside a firewall to a VPN server inside, the firewall would need to allow the following protocols:

|**Protocol**|**Port**|**Description**|
|---|---|---|
|`Internet Protocol` (`IP`)|`UDP/50-51`|This is the primary protocol that provides the foundation for all internet communication. It is used to route packets of data between the VPN client and the VPN server.|
|`Internet Key Exchange` (`IKE`)|`UDP/500`|IKE is a protocol that is used to establish and maintain secure communication between the VPN client and the VPN server. It is based on the Diffie-Hellman key exchange algorithm, and it is used to negotiate and establish shared secret keys that can be used to encrypt and decrypt the VPN traffic.|
|`Encapsulating Security Payload` (`ESP`)|`UDP/4500`|ESP is also a protocol that provides encryption and authentication for IP datagrams. It is used to encrypt the VPN traffic between the VPN client and the VPN server, using the keys that were negotiated with IKE.|

These protocols are necessary for facilitating IPsec VPN traffic because they provide the security and encryption that are required for secure communication over the public internet. Without these protocols, the VPN traffic would be vulnerable to interception and tampering.