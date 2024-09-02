---
tags:
  - Networking
  - Protocols
---
Open Systems Interconnection model

![[Pasted image 20240507090109.png]]

|**Layer**|**Function**|
|---|---|
|`7.Application`|Among other things, this layer controls the input and output of data and provides the application functions.|
|`6.Presentation`|The presentation layer's task is to transfer the system-dependent presentation of data into a form independent of the application.|
|`5.Session`|The session layer controls the logical connection between two systems and prevents, for example, connection breakdowns or other problems.|
|`4.Transport`|Layer 4 is used for end-to-end control of the transferred data. The Transport Layer can detect and avoid congestion situations and segment data streams.|
|`3.Network`|On the networking layer, connections are established in circuit-switched networks, and data packets are forwarded in packet-switched networks. Data is transmitted over the entire network from the sender to the receiver.|
|`2.Data Link`|The central task of layer 2 is to enable reliable and error-free transmissions on the respective medium. For this purpose, the bitstreams from layer 1 are divided into blocks or frames.|
|`1.Physical`|The transmission techniques used are, for example, electrical signals, optical signals, or electromagnetic waves. Through layer 1, the transmission takes place on wired or wireless transmission lines|
The `TCP/IP` (`Transmission Control Protocol` (`TCP`) and `Internet Protocol` (`IP`)) model is also a layered reference model, often referred to as the `Internet Protocol Suite`. 

|**Layer**|**Function**|
|---|---|
|`4.Application`|The Application Layer allows applications to access the other layers' services and defines the protocols applications use to exchange data.|
|`3.Transport`|The Transport Layer is responsible for providing (TCP) session and (UDP) datagram services for the Application Layer.|
|`2.Internet`|The Internet Layer is responsible for host addressing, packaging, and routing functions.|
|`1.Link`|The Link layer is responsible for placing the TCP/IP packets on the network medium and receiving corresponding packets from the network medium. TCP/IP is designed to work independently of the network access method, frame format, and medium.|
## ISO/OSI vs. TCP/IP

`TCP/IP` is a communication protocol that allows hosts to connect to the Internet. It refers to the `Transmission Control Protocol` used in and by applications on the Internet. In contrast to `OSI`, it allows a lightening of the rules that must be followed, provided that general guidelines are followed.

`OSI`, on the other hand, is a communication gateway between the network and end-users. The OSI model is usually referred to as the reference model because it is newer and more widely used. It is also known for its strict protocol and limitations.

# Protocol Data Unit (PDU)

![[Pasted image 20240507090421.png]]