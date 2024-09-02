---
tags:
  - Networking
  - Protocols
---

[TCP Protocol](https://tools.ietf.org/html/rfc793)
[UDP Protocol](https://tools.ietf.org/html/rfc768)

The Transport Layer has several mechanisms to help ensure the seamless delivery of data from source to destination. Think about the Transport layer as a control hub. Application data from the higher layers have to traverse down the stack to the Transport layer. This layer directs how the traffic will be encapsulated and thrown to the lower layer protocols ( IP and MAC ). Once the data reaches its intended recipient, the Transport layer, working with the Network / Internet layer protocols, is responsible for reassembling the encapsulated data back in the correct order. The two mechanisms used to accomplish this task are the Transmission Control (`TCP`) and the User Datagram Protocol (`UDP`).

#### TCP VS. UDP

| **Characteristic**         | **TCP**                                                                    | **UDP**                                                                 |
| -------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `Transmission`             | Connection-oriented                                                        | Connectionless. Fire and forget.                                        |
| `Connection Establishment` | TCP uses a three-way handshake to ensure that a connection is established. | UDP does not ensure the destination is listening.                       |
| `Data Delivery`            | Stream-based conversations                                                 | packet by packet, the source does not care if the destination is active |
| `Receipt of data`          | Sequence and Acknowledgement numbers are utilized to account for data.     | UDP does not care.                                                      |
| `Speed`                    | TCP has more overhead and is slower because of its built-in functions.     | UDP is fast but unreliable.                                             |

## TCP Three-way Handshake

One of the ways TCP ensures the delivery of data from server to client is the utilization of sessions. These sessions are established through what is called a three-way handshake. To make this happen, TCP utilizes an option in the TCP header called flags. We will not deep dive into TCP flags now; know that the common flags we will see in a three-way handshake are Synchronization (`SYN`) and acknowledgment (`ACK`). When a host requests to have a conversation with a server over TCP;

1. The `client` sends a packet with the SYN flag set to on along with other negotiable options in the TCP header.
    
    1. This is a synchronization packet. It will only be set in the first packet from host and server and enables establishing a session by allowing both ends to agree on a sequence number to start communicating with.
    2. This is crucial for the tracking of packets. Along with the sequence number sync, many other options are negotiated in this phase to include window size, maximum segment size, and selective acknowledgments.
2. The `server` will respond with a TCP packet that includes a SYN flag set for the sequence number negotiation and an ACK flag set to acknowledge the previous SYN packet sent by the host.
    
    1. The server will also include any changes to the TCP options it requires set in the options fields of the TCP header.
3. The `client` will respond with a TCP packet with an ACK flag set agreeing to the negotiation.
    
    1. This packet is the end of the three-way handshake and established the connection between client and server.


Before session termination, we should see a packet pattern of:
1. `FIN, ACK`
2. `FIN, ACK`,
3. `ACK`

|**Flags**|**Description**|
|---|---|
|`URG (Urgent)`|This flag is to denote urgency with the current data in stream.|
|`ACK (Acknowledgement)`|This flag acknowledges receipt of data.|
|`PSH (Push)`|This flag instructs the TCP stack to immediately deliver the received data to the application layer, and bypass buffering.|
|`RST (Reset)`|This flag is used for termination of the TCP connection (we will dive into hijacking and RST attacks soon).|
|`SYN (Synchronize)`|This flag is used to establish an initial connection with TCP.|
|`FIN (Finish)`|This flag is used to denote the finish of a TCP connection. It is used when no more data needs to be sent.|
|`ECN (Explicit Congestion Notification)`|This flag is used to denote congestion within our network, it is to let the hosts know to avoid unnecessary re-transmissions.|