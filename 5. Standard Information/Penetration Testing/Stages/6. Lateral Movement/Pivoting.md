---
tags:
  - PenetrationTesting
  - Stages
  - LateralMovement
  - StandardInformation
---
In most cases, the system we use will not have the tools to enumerate the internal network efficiently. Some techniques allow us to use the exploited host as a proxy and perform all the scans from our attack machine or VM. In doing so, the exploited system represents and routes all our network requests sent from our attack machine to the internal network and its network components.

In this way, we make non-routable networks (and therefore publicly unreachable) can still be reached. This allows us to scan them for vulnerabilities and penetrate deeper into the network. This process is also known as `Pivoting` or `Tunneling`.

When looking for opportunities to pivot, it can be helpful to look at the hosts' routing table to identify which networks we may be able to reach or which routes we may need to add.
##### Example

During one tricky engagement, the target had their network physically and logically separated. This separation made it difficult for us to move around and complete our objectives. We had to search the network and compromise a host that turned out to be the engineering workstation used to maintain and monitor equipment in the operational environment, submit reports, and perform other administrative duties in the enterprise environment. That host turned out to be dual-homed (having more than one physical NIC connected to different networks). Without it having access to both enterprise and operational networks, we would not have been able to pivot as we needed to complete our assessment.