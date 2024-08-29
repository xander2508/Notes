Network Mapper (`Nmap`) is an open-source network analysis and security auditing tool written in C, C++, Python, and Lua. It is designed to scan networks and identify which hosts are available on the network using raw packets, and services and applications, including the name and version, where possible. It can also identify the operating systems and versions of these hosts. Besides other features, Nmap also offers scanning capabilities that can determine if packet filters, firewalls, or intrusion detection systems (IDS) are configured as needed.

## Use Cases

The tool is one of the most used tools by network administrators and IT security specialists. It is used to:

- Audit the security aspects of networks
- Simulate penetration tests
- Check firewall and IDS settings and configurations
- Types of possible connections
- Network mapping
- Response analysis
- Identify open ports
- Vulnerability assessment as well.

#### Host Discovery

[Putting It All Together: Host Discovery Strategies | Nmap Network Scanning](https://nmap.org/book/host-discovery-strategies.html)

## Nmap Architecture

Nmap offers many different types of scans that can be used to obtain various results about our targets. Basically, Nmap can be divided into the following scanning techniques:

- Host discovery
- Port scanning
- Service enumeration and detection
- OS detection
- Scriptable interaction with the target service (Nmap Scripting Engine)

## Syntax

```shell-session
nmap <scan types> <options> <target>
```

#### SYN Scan 

- If our target sends an `SYN-ACK` flagged packet back to the scanned port, Nmap detects that the port is `open`.
- If the packet receives an `RST` flag, it is an indicator that the port is `closed`.
- If Nmap does not receive a packet back, it will display it as `filtered`. Depending on the firewall configuration, certain packets may be dropped or ignored by the firewall.
- See [[Types#Excessive SYN Flags]]

```shell-session
sudo nmap -sS
```

#### Disable Port Scanning

Detect which hosts are open.

```shell-session
sudo nmap -sn 10.129.2.0/24
```

#### Scan from IP List

```shell-session
sudo nmap -iL hosts.txt
```

#### Ping scan

```shell-session
sudo nmap 10.129.2.18 -PE
```

#### Packet Trace 

```shell-session
sudo nmap 10.129.2.18 --packet-trace 
```

#### Reason for Alive

Another way to determine why Nmap has our target marked as "alive" is with the "`--reason`" option.

```shell-session
sudo nmap 10.129.2.18 --reason 
```

#### Disable ARP Ping 

```shell-session
 sudo nmap 10.129.2.18 --disable-arp-ping 
```
# Command Examples

1. `nmap -sV -sT -sC arkham.htb`
