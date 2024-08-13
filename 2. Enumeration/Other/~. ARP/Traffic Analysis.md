
See [[1. Analysis Overview]]

Within [[Wireshark]]:

# Guide

Filter ARP packets with:
```
arp.opcode
```


The opcode functionality in `Wireshark` can simplify this process.

1. `Opcode == 1`: This represents all types of ARP Requests
2. `Opcode == 2`: This signifies all types of ARP Replies