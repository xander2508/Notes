The Transport Layer has several mechanisms to help ensure the seamless delivery of data from source to destination. Think about the Transport layer as a control hub. Application data from the higher layers have to traverse down the stack to the Transport layer. This layer directs how the traffic will be encapsulated and thrown to the lower layer protocols ( IP and MAC ). Once the data reaches its intended recipient, the Transport layer, working with the Network / Internet layer protocols, is responsible for reassembling the encapsulated data back in the correct order. The two mechanisms used to accomplish this task are the Transmission Control (`TCP`) and the User Datagram Protocol (`UDP`).

#### TCP VS. UDP

| **Characteristic**         | **TCP**                                                                    | **UDP**                                                                 |
| -------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `Transmission`             | Connection-oriented                                                        | Connectionless. Fire and forget.                                        |
| `Connection Establishment` | TCP uses a three-way handshake to ensure that a connection is established. | UDP does not ensure the destination is listening.                       |
| `Data Delivery`            | Stream-based conversations                                                 | packet by packet, the source does not care if the destination is active |
| `Receipt of data`          | Sequence and Acknowledgement numbers are utilized to account for data.     | UDP does not care.                                                      |
| `Speed`                    | TCP has more overhead and is slower because of its built-in functions.     | UDP is fast but unreliable.                                             |

