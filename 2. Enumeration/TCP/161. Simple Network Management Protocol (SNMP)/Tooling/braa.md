Once we know a community string, we can use it with [braa](https://github.com/mteg/braa) to brute-force the individual OIDs and enumerate the information behind them.

Braa is a mass SNMP scanner. The intended usage of such a tool is of course 
making SNMP queries it is able to query dozens or hundreds of hosts simultaneously, and in a single process. Thus, it consumes very few system resources and does the scanning VERY fast.
  
Braa implements its OWN SNMP stack, so it does NOT need any SNMP libraries
like net-SNMP. The implementation is very dirty, supports only several data
types, and in any case cannot be stated 'standard-conforming'! There is no ASN.1 parser in braa - you HAVE to know the numerical
values of OID's (for instance .1.3.6.1.2.1.1.5.0 instead of system.sysName.0).

## Installation 

```shell-session
sudo apt install braa
```

## Usage

```bash
braa <community string>@<IP>:.1.3.6.*   # Syntax
```

```bash
braa public@10.129.14.128:.1.3.6.*
```