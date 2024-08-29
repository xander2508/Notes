
## Excessive SYN Flags

Simply put, the adversary will send TCP SYN packets to the target ports. In the case where our port is open, our machine will respond with a SYN-ACK packet to continue the handshake, which will then be met by an RST from the attackers scanner. However, we can get lost in the RSTs here as our machine will respond with RST for closed ports.

1. `SYN Scans` - In these scans the behaviour will be as we see, however the attacker will pre-emptively end the handshake with the RST flag.
2. `SYN Stealth Scans` - In this case the attacker will attempt to evade detection by only partially completing the TCP handshake.

## No Flags

On the opposite side of things, the attacker might send no flags. This is what is commonly referred to as a NULL scan. In a NULL scan an attacker sends TCP packets with no flags. TCP connections behave like the following when a NULL packet is received.

1. `If the port is open` - The system will not respond at all since there is no flags.
    
2. `If the port is closed` - The system will respond with an RST packet.

## Too Many ACKs

On the other hand, we might notice an excessive amount of acknowledgements between two hosts. In this case the attacker might be employing the usage of an ACK scan. In the case of an ACK scan TCP connections will behave like the following.

1. `If the port is open` - The affected machine will either not respond, or will respond with an RST packet.
    
2. `If the port is closed` - The affected machine will respond with an RST packet.

## Excessive FINs

Using another part of the handshake, an attacker might utilize a FIN scan. In this case, all TCP packets will be marked with the FIN flag. We might notice the following behavior from our affected machine.

1. `If the port is open` - Our affected machine simply will not respond.
    
2. `If the port is closed` - Our affected machine will respond with an RST packet.

## Just too many flags

Let's say the attacker just wanted to throw spaghetti at the wall. In that case, they might utilize a Xmas tree scan, which is when they put all TCP flags on their transmissions. Similarly, our affected host might respond like the following when all flags are set.

1. `If the port is open` - The affected machine will not respond, or at least it will with an RST packet.
    
2. `If the port is closed` - The affected machine will respond with an RST packet.