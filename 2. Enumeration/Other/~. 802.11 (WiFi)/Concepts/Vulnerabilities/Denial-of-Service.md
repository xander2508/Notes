## Deauthentication Attacks

Among the more frequent attacks we might witness or detect is a deauthentication/dissociation attack. This is a commonplace link-layer precursor attack that adversaries might employ for several reasons:

1. `To capture the WPA handshake to perform an offline dictionary attack`
2. `To cause general denial of service conditions`
3. `To enforce users to disconnect from our network, and potentially join their network to retrieve information`

In essence, the attacker will fabricate an 802.11 deauthentication frame pretending it originates from our legitimate access point. By doing so, the attacker might manage to disconnect one of our clients from the network. Often, the client will reconnect and go through the handshake process while the attacker is sniffing.