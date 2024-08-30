

## Scan Types

| Option   | Description                                                                                           |
| -------- | ----------------------------------------------------------------------------------------------------- |
| -O       | Scan for operating system                                                                             |
| -p / -p- | Select port / All ports                                                                               |
| -sS      | SYN Scan, see [[Types#Excessive SYN Flags\|SYN Type]]                                                 |
| -sA      | ACK Scan, see [[Types#Too Many ACKs\|ACK Type]]. `unfiltered` may mean open in the case of this scan. |
| -sV      | Version Scan, detect versions of services                                                             |
| -sU      | UDP Scan                                                                                              |
| -sT      | Connect Scan, see [[Types#Connect Type]]                                                              |
| -PE      | Ping Scan, ICMP ping echo scan                                                                        |
| -sn      | Disable port scanning                                                                                 |

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

# Extra Features

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

## Output Formats

- Normal output (`-oN`) with the `.nmap` file extension
- Greppable output (`-oG`) with the `.gnmap` file extension
- XML output (`-oX`) with the `.xml` file extension
- `-oA target` Saves the results in all formats, starting the name of each file with 'target'.

## Performance

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
