[TCPDump](https://www.tcpdump.org/) is a command-line utility that, with the aid of LibPcap, captures and interprets network traffic from a network interface or capture file. 

It was built for use on any Unix-like operating system and had a Windows twin called `WinDump`. It is a potent and straightforward tool used on most Unix-based systems. It does not require a GUI and can be used through any terminal or remote connection, such as SSH.

To capture network traffic from "off the wire," it uses the libraries `pcap` and `libpcap`, paired with an interface in promiscuous mode to listen for data. This allows the program to see and capture packets sourcing from or destined for any device in the local area network, not just the packets destined for us.

TCPDump is available for most Unix systems and Unix derivatives, such as AIX, BSD, Linux, Solaris, and is supplied by many manufacturers already in the system. Due to the direct access to the hardware, we need the `root` or the `administrator's` privileges to run this tool. For us that means we will have to utilize `sudo` to execute TCPDump as seen in the examples below. `TCPDump` often comes preinstalled on the majority of Linux operating systems.

Theoretically, we can use `tcpdump` to create an IDS/IPS system by having a Bash script analyze the intercepted packets according to a specific pattern. We can then set conditions to, for example, ban a particular IP address that has sent too many ICMP echo requests for a certain period.
#### Install Tcpdump

```
which tcpdump
```

```shell-session
sudo apt install tcpdump 
```
#### Usage

```
tcpdump -i any -w log.pcap
```

#### Basic Capture Options

These switches can be chained together to craft how the tool output is shown to us in STDOUT and what is saved to the capture file. This is not an exhaustive list, and there are many more we can use, but these are the most common and valuable.

| **Switch Command** | **Result**                                                                                                         |
| :----------------: | ------------------------------------------------------------------------------------------------------------------ |
|         D          | Will display any interfaces available to capture from.                                                             |
|         i          | Selects an interface to capture from. ex. -i eth0                                                                  |
|         n          | Do not resolve hostnames.                                                                                          |
|         nn         | Do not resolve hostnames or well-known ports.                                                                      |
|         e          | Will grab the ethernet header along with upper-layer data.                                                         |
|         X          | Show Contents of packets in hex and ASCII.                                                                         |
|         XX         | Same as X, but will also specify ethernet headers. (like using Xe)                                                 |
|     v, vv, vvv     | Increase the verbosity of output shown and saved.                                                                  |
|         c          | Grab a specific number of packets, then quit the program.                                                          |
|         s          | Defines how much of a packet to grab.                                                                              |
|         S          | change relative sequence numbers in the capture display to absolute sequence numbers. (13248765839 instead of 101) |
|         q          | Print less protocol information.                                                                                   |
|    r file.pcap     | Read from a file.                                                                                                  |
|    w file.pcap     | Write into a file                                                                                                  |
![[breakdown.webp]]

|**Filter**|**Result**|
|---|---|
|Timestamp|`Yellow` The timestamp field comes first and is configurable to show the time and date in a format we can ingest easily.|
|Protocol|`Orange` This section will tell us what the upper-layer header is. In our example, it shows IP.|
|Source & Destination IP.Port|`Orange` This will show us the source and destination of the packet along with the port number used to connect. Format == `IP.port == 172.16.146.2.21`|
|Flags|`Green` This portion shows any flags utilized.|
|Sequence and Acknowledgement Numbers|`Red` This section shows the sequence and acknowledgment numbers used to track the TCP segment. Our example is utilizing low numbers to assume that relative sequence and ack numbers are being displayed.|
|Protocol Options|`Blue` Here, we will see any negotiated TCP values established between the client and server, such as window size, selective acknowledgments, window scale factors, and more.|
|Notes / Next Header|`White` Misc notes the dissector found will be present here. As the traffic we are looking at is encapsulated, we may see more header information for different protocols. In our example, we can see the TCPDump dissector recognizes FTP traffic within the encapsulation to display it for us.|