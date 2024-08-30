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

## Scan Options

#### Scan for Operating System

```
nmap 10.0.0.0 -O
```
#### Scan All Ports 

```
nmap 10.0.0.0 -p-
```
#### SYN Scan 

- If our target sends an `SYN-ACK` flagged packet back to the scanned port, Nmap detects that the port is `open`.
- If the packet receives an `RST` flag, it is an indicator that the port is `closed`.
- If Nmap does not receive a packet back, it will display it as `filtered`. Depending on the firewall configuration, certain packets may be dropped or ignored by the firewall.
- See [[Types#Excessive SYN Flags]]

```shell-session
sudo nmap -sS
```

#### ACK Scan

Nmap's TCP ACK scan (`-sA`) method is much harder to filter for firewalls and IDS/IPS systems than regular SYN (`-sS`) or Connect scans (`sT`) because they only send a TCP packet with only the `ACK` flag. When a port is closed or open, the host must respond with an `RST` flag. Unlike outgoing connections, all connection attempts (with the `SYN` flag) from external networks are usually blocked by firewalls. However, the packets with the `ACK` flag are often passed by the firewall because the firewall cannot determine whether the connection was first established from the external network or the internal network.

```shell-session
 sudo nmap 10.129.2.28 -p- -sA 
```

`unfiltered` may mean open in the case of this scan. This can be shown in the packet trace because open ports must respond with `RST`.
#### Disable Port Scanning

Detect which hosts are open.

```shell-session
sudo nmap -sn 10.129.2.0/24
```

#### Ping scan

```shell-session
sudo nmap 10.129.2.18 -PE
```
#### Connect Scan

The Nmap [TCP Connect Scan](https://nmap.org/book/scan-methods-connect-scan.html) (`-sT`) uses the TCP three-way handshake to determine if a specific port on a target host is open or closed. The scan sends an `SYN` packet to the target port and waits for a response. It is considered open if the target port responds with an `SYN-ACK` packet and closed if it responds with an `RST` packet.

The `Connect` scan is useful because it is the most accurate way to determine the state of a port, and it is also the most stealthy. Unlike other types of scans, such as the SYN scan, the Connect scan does not leave any unfinished connections or unsent packets on the target host, which makes it less likely to be detected by intrusion detection systems (IDS) or intrusion prevention systems (IPS). It is useful when we want to map the network and don't want to disturb the services running behind it, thus causing a minimal impact and sometimes considered a more polite scan method.

```shell-session
sudo nmap 10.129.2.28 -p 443 -sT 
```
#### UDP Scan

```shell-session
sudo nmap 10.129.2.28 -p 86 -sU
```

#### Version Scan 

```shell-session
sudo nmap 10.129.2.28 -p 445 --reason  -sV
```

#### [[Decoy Scanning]]

With this method, we can generate random (`RND`) a specific number (for example: `5`) of IP addresses separated by a colon (`:`). Our real IP address is then randomly placed between the generated IP addresses. In the next example, our real IP address is therefore placed in the second position. Another critical point is that the decoys must be alive. Otherwise, the service on the target may be unreachable due to SYN-flooding security mechanisms.

```shell-session
 sudo nmap 10.129.2.28 -p 80 -sS -D RND:5
```

```shell-session
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-21 16:14 CEST
SENT (0.0378s) TCP 102.52.161.59:59289 > 10.129.2.28:80 S ttl=42 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460>
SENT (0.0378s) TCP 10.10.14.2:59289 > 10.129.2.28:80 S ttl=59 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460>
SENT (0.0379s) TCP 210.120.38.29:59289 > 10.129.2.28:80 S ttl=37 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460>
SENT (0.0379s) TCP 191.6.64.171:59289 > 10.129.2.28:80 S ttl=38 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460>
SENT (0.0379s) TCP 184.178.194.209:59289 > 10.129.2.28:80 S ttl=39 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460>
SENT (0.0379s) TCP 43.21.121.33:59289 > 10.129.2.28:80 S ttl=55 id=29822 iplen=44  seq=3687542010 win=1024 <mss 1460>
RCVD (0.1370s) TCP 10.129.2.28:80 > 10.10.14.2:59289 SA ttl=64 id=0 iplen=44  seq=4056111701 win=64240 <mss 1460>
Nmap scan report for 10.129.2.28
Host is up (0.099s latency).
```
## Extra Features

#### DNS Proxying

`Nmap` gives us a way to specify DNS servers ourselves (`--dns-server <ns>,<ns>`). 

This method could be fundamental to us if we are in a demilitarized zone (`DMZ`). The company's DNS servers are usually more trusted than those from the Internet. So, for example, we could use them to interact with the hosts of the internal network.

#### Modify Source Address 

We can use `TCP port 53` as a source port (`--source-port`) for our scans. If the administrator uses the firewall to control this port and does not filter IDS/IPS properly, our TCP packets will be trusted and passed through. This is because DNS utilises these ports and is normally more trusted.
#### Spoof Source Address 

A possible use of this flag is to spoof the scan to make the targets think that _someone else_ is scanning them. Imagine a company being repeatedly port scanned by a competitor! The `-e` option and `-Pn` are generally required for this sort of usage. Note that you usually won't receive reply packets back (they will be addressed to the IP you are spoofing), so Nmap won't produce useful reports.

```shell-session
sudo nmap 10.129.2.28 -Pn -p 445 -S 10.129.2.200 -e tun0
```
#### Scan from IP List

```shell-session
sudo nmap -iL hosts.txt
```
#### Packet Trace 

This allows us to see the specific information sent and received. This allows us to make educated guesses regarding sates of ports. 

If we receive an `ICMP` reply with `type 3` and `error code 3`, which indicates that the desired port is unreachable. Nevertheless, if we know that the host is alive, we can strongly assume that the firewall on this port is rejecting the packets, and we will have to take a closer look at this port later.

It may also show us more information from port banners than shown with just `-sV`. It just takes a bit more reading.

```shell-session
sudo nmap 10.129.2.18 --packet-trace 
```
#### Reason for Alive

Another way to determine why Nmap has our target marked as "alive" is with the "`--reason`" option.

```shell-session
sudo nmap 10.129.2.18 --reason 
```
#### Disable Features

| `-n`                 | Disables DNS resolution. |
| -------------------- | ------------------------ |
| `--disable-arp-ping` | Disables ARP ping.       |
| `-Pn`                | Disable ICMP echo        |
#### Top 100 Ports

| `-F` | Scans top 100 ports. |
| ---- | -------------------- |

#### Output Formats

- Normal output (`-oN`) with the `.nmap` file extension
- Greppable output (`-oG`) with the `.gnmap` file extension
- XML output (`-oX`) with the `.xml` file extension
- `-oA target` Saves the results in all formats, starting the name of each file with 'target'.

#### Performance

[Timing and Performance | Nmap Network Scanning](https://nmap.org/book/man-performance.html)

| Option                                                                             | Description                     |
| ---------------------------------------------------------------------------------- | ------------------------------- |
| `-T <0-5>`                                                                         | How fast                        |
| `--min-parallelism <number>`                                                       | How frequent                    |
| `--max-rtt-timeout <time>`/`--min-RTT-timeout <time>`/`--initial-rtt-timeout 50ms` | Timeouts of packets             |
| `--min-rate <number>`                                                              | How many packets simultaneously |
| `--max-retries <number>`                                                           | Max retries                     |

`Nmap` offers six different timing templates (`-T <0-5>`) for us to use. These values (`0-5`) determine the aggressiveness of our scans. This can also have negative effects if the scan is too aggressive, and security systems may block us due to the produced network traffic. The default timing template used when we have defined nothing else is the normal (`-T 3`).

- `-T 0` / `-T paranoid`
- `-T 1` / `-T sneaky`
- `-T 2` / `-T polite`
- `-T 3` / `-T normal`
- `-T 4` / `-T aggressive`
- `-T 5` / `-T insane`

The exact used options with their values we can find here: [https://nmap.org/book/performance-timing-templates.html](https://nmap.org/book/performance-timing-templates.html)

|                                                   | T0                                        | T1         | T2         | T3         | T4         | T5         |
| ------------------------------------------------- | ----------------------------------------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| Name                                              | Paranoid                                  | Sneaky     | Polite     | Normal     | Aggressive | Insane     |
| `min-rtt-timeout`                                 | 100 ms                                    | 100 ms     | 100 ms     | 100 ms     | 100 ms     | 50 ms      |
| `max-rtt-timeout`                                 | 5 minutes                                 | 15 seconds | 10 seconds | 10 seconds | 1250 ms    | 300 ms     |
| `initial-rtt-timeout`                             | 5 minutes                                 | 15 seconds | 1 second   | 1 second   | 500 ms     | 250 ms     |
| `max-retries`                                     | 10                                        | 10         | 10         | 10         | 6          | 2          |
| Initial (and minimum) scan delay (`--scan-delay`) | 5 minutes                                 | 15 seconds | 400 ms     | 0          | 0          | 0          |
| Maximum TCP scan delay                            | 5 minutes                                 | 15,000     | 1 second   | 1 second   | 10 ms      | 5 ms       |
| Maximum UDP scan delay                            | 5 minutes                                 | 15 seconds | 1 second   | 1 second   | 1 second   | 1 second   |
| `host-timeout`                                    | 0                                         | 0          | 0          | 0          | 0          | 15 minutes |
| `script-timeout`                                  | 0                                         | 0          | 0          | 0          | 0          | 10 minutes |
| `min-parallelism`                                 | Dynamic, not affected by timing templates |            |            |            |            |            |
| `max-parallelism`                                 | 1                                         | 1          | 1          | Dynamic    | Dynamic    | Dynamic    |
| `min-hostgroup`                                   | Dynamic, not affected by timing templates |            |            |            |            |            |
| `max-hostgroup`                                   | Dynamic, not affected by timing templates |            |            |            |            |            |
| `min-rate`                                        | No minimum rate limit                     |            |            |            |            |            |
| `max-rate`                                        | No maximum rate limit                     |            |            |            |            |            |
| `defeat-rst-ratelimit`                            | Not enabled by default                    |            |            |            |            |            |
## Results 

| **State**          | **Description**                                                                                                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `open`             | This indicates that the connection to the scanned port has been established. These connections can be **TCP connections**, **UDP datagrams** as well as **SCTP associations**.                          |
| `closed`           | When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an `RST` flag. This scanning method can also be used to determine if our target is alive or not. |
| `filtered`         | Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.                  |
| `unfiltered`       | This state of a port only occurs during the **TCP-ACK** scan and means that the port is accessible, but it cannot be determined whether it is open or closed.                                           |
| `open\|filtered`   | If we do not get a response for a specific port, `Nmap` will set it to that state. This indicates that a firewall or packet filter may protect the port.                                                |
| `closed\|filtered` | This state only occurs in the **IP ID idle** scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.                                           |

# Command Examples

1. `nmap -sV -sT -sC arkham.htb`
