
Each host in a network has its own `48`-bit (`6 octets`) `Media Access Control` (`MAC`) address, represented in hexadecimal format. `MAC` is the `physical address` for our network interfaces. There are several different standards for the MAC address:

|**Representation**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**5th Octet**|**6th Octet**|
|---|---|---|---|---|---|---|
|Binary|1101 1110|1010 1101|1011 1110|1110 1111|0001 0011|0011 0111|
|Hex|DE|AD|BE|EF|13|37|

The MAC address consists of a total of `6 bytes`. The first half (`3 bytes` / `24 bit`) is the so-called `Organization Unique Identifier` (`OUI`) defined by the `Institute of Electrical and Electronics Engineers` (`IEEE`) for the respective manufacturers.

As with IPv4 addresses, there are also certain reserved areas for the MAC address. These include, for example, the local range for the MAC.

|**Local Range**|
|---|
|0`2`:00:00:00:00:00|
|0`6`:00:00:00:00:00|
|0`A`:00:00:00:00:00|
|0`E`:00:00:00:00:00|
Furthermore, the last two bits in the first octet can play another essential role. The last bit can have two states, 0 and 1, as we already know. The last bit identifies the MAC address as `Unicast` (`0`) or `Multicast` (`1`). With `unicast`, it means that the packet sent will reach only one specific host.
#### MAC Unicast

|**Representation**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**5th Octet**|**6th Octet**|
|---|---|---|---|---|---|---|
|Binary|1101 111`0`|1010 1101|1011 1110|1110 1111|0001 0011|0011 0111|
|Hex|D`E`|
#### MAC Multicast

|**Representation**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**5th Octet**|**6th Octet**|
|---|---|---|---|---|---|---|
|Binary|`0000 0001`|`0000 0000`|`0101 1110`|1110 1111|0001 0011|0011 0111|
|Hex|`01`|`00`|`5E`|EF|13|37|
#### MAC Broadcast

|**Representation**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**5th Octet**|**6th Octet**|
|---|---|---|---|---|---|---|
|Binary|`1111 1111`|`1111 1111`|`1111 1111`|`1111 1111`|`1111 1111`|`1111 1111`|
|Hex|
The second last bit in the first octet identifies whether it is a `global OUI`, defined by the IEEE, or a `locally administrated` MAC address.

#### Global OUI

|**Representation**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**5th Octet**|**6th Octet**|
|---|---|---|---|---|---|---|
|Binary|1101 11`0`0|1010 1101|1011 1110|1110 1111|0001 0011|0011 0111|
|Hex|D`C`|AD|BE|EF|13|37|

#### Locally Administrated

|**Representation**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**5th Octet**|**6th Octet**|
|---|---|---|---|---|---|---|
|Binary|1101 11`1`0|1010 1101|1011 1110|1110 1111|0001 0011|0011 0111|
|Hex|


- `MAC spoofing`: This involves altering the MAC address of a device to match that of another device, typically to gain unauthorized access to a network.
    
- `MAC flooding`: This involves sending many packets with different MAC addresses to a network switch, causing it to reach its MAC address table capacity and effectively preventing it from functioning correctly.
    
- `MAC address filtering`: Some networks may be configured only to allow access to devices with specific MAC addresses that we could potentially exploit by attempting to gain access to the network using a spoofed MAC address.