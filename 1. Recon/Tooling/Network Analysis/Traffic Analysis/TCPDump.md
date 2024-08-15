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

| **Switch Command** | **Result**                                                                                                                                                                                 |
| :----------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|         D          | Will display any interfaces available to capture from.                                                                                                                                     |
|         i          | Selects an interface to capture from. ex. -i eth0                                                                                                                                          |
|         n          | Do not resolve hostnames.                                                                                                                                                                  |
|         nn         | Do not resolve hostnames or well-known ports.                                                                                                                                              |
|         e          | Will grab the ethernet header along with upper-layer data.                                                                                                                                 |
|         X          | Show Contents of packets in hex and ASCII.                                                                                                                                                 |
|         XX         | Same as X, but will also specify ethernet headers. (like using Xe)                                                                                                                         |
|     v, vv, vvv     | Increase the verbosity of output shown and saved.                                                                                                                                          |
|         c          | Grab a specific number of packets, then quit the program.                                                                                                                                  |
|         s          | Defines how much of a packet to grab.                                                                                                                                                      |
|         S          | change relative sequence numbers in the capture display to absolute sequence numbers. (13248765839 instead of 101)                                                                         |
|         q          | Print less protocol information.                                                                                                                                                           |
|    r file.pcap     | Read from a file.                                                                                                                                                                          |
|    w file.pcap     | Write into a file                                                                                                                                                                          |
|         l          | Make stdout line buffered.  Useful if you want to see the data while capturing it<br>``` <br>tcpdump -l \| tee dat<br>```<br>```<br>sudo tcpdump -Ar http.cap -l \| grep 'mailto:*'<br>``` |
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


## Filtering 

See [Berkeley packet filters - IBM Documentation](https://www.ibm.com/docs/en/qsip/7.4?topic=queries-berkeley-packet-filters)

#### Helpful TCPDump Filters

| **Filter**           | **Result**                                                                                                                                                                                                                                                                                                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| host                 | `host` will filter visible traffic to show anything involving the designated host. Bi-directional<br><br><br> `Syntax: host [IP]`<br>```shell-session<br>sudo tcpdump -i eth0 host 172.16.146.2<br>```                                                                                                                                                                                                  |
| src / dest           | `src` and `dest` are modifiers. We can use them to designate a source or destination host or port.<br><br>`Syntax: src/dst [host\|net\|port] [IP\|Network Range\|Port]`<br>```shell-session<br>sudo tcpdump -i eth0 src host 172.16.146.2<br>```<br><br>```shell-session<br>sudo tcpdump -i eth0 tcp src port 80<br>```<br><br>```shell-session<br>sudo tcpdump -i eth0 dest net 172.16.146.0/24<br>``` |
| net                  | `net` will show us any traffic sourcing from or destined to the network designated. It uses / notation.<br><br>```shell-session<br>sudo tcpdump -i eth0 dest net 172.16.146.0/24<br>```                                                                                                                                                                                                                 |
| proto                | will filter for a specific protocol type. (ether, TCP, UDP, and ICMP as examples)<br><br>`Syntax: [tcp/udp/icmp]`<br>```shell-session<br>sudo tcpdump -i eth0 udp<br>```                                                                                                                                                                                                                                |
| port                 | `port` is bi-directional. It will show any traffic with the specified port as the source or destination.<br><br><br>`Syntax: port [port number]`<br>```<br>sudo tcpdump -i eth0 tcp port 443<br>```                                                                                                                                                                                                     |
| portrange            | `portrange` allows us to specify a range of ports. (0-1024)<br>```shell-session<br>Syntax: portrange [portrange 0-65535]<br>```<br>```shell-session<br>sudo tcpdump -i eth0 portrange 0-1024<br>```                                                                                                                                                                                                     |
| less / greater "< >" | `less` and `greater` can be used to look for a packet or protocol option of a specific size.<br><br>```shell-session<br>Syntax: less/greater [size in bytes]<br>```<br>```shell-session<br>sudo tcpdump -i eth0 less 64<br>```<br>```shell-session<br>sudo tcpdump -i eth0 greater 500<br>```                                                                                                           |
| and / &&             | `and` `&&` can be used to concatenate two different filters together. for example, src host AND port.<br><br>```shell-session<br>Syntax: and [requirement]<br>```<br>```shell-session<br>sudo tcpdump -i eth0 host 192.168.0.1 and port 23<br>```<br>                                                                                                                                                   |
| or                   | `or` allows for a match on either of two conditions. It does not have to meet both. It can be tricky.<br><br>```shell-session<br>sudo tcpdump -r sus.pcap icmp or host 172.16.146.1<br>```                                                                                                                                                                                                              |
| not                  | `not` is a modifier saying anything but x. For example, not UDP.<br><br>```shell-session<br>sudo tcpdump -r sus.pcap not icmp<br>```<br>                                                                                                                                                                                                                                                                |

### Filtering Packet Internals 

We can dig as deep as we wish into the packets we captured. It requires a bit of knowledge of how the protocols are structured, however. For example, if we wanted to see only packets with the TCP SYN flag set, we could use the following command:

```shell-session
sudo tcpdump -i eth0 'tcp[13] &2 != 0'
```

This is counting to the 13th byte in the structure and looking at the 2nd bit. If it is set to 1 or ON, the SYN flag is set.

## Notes

1. Turning absolute sequence numbers on `(-S)` will be extremely helpful in determining conversations.