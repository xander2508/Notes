## Deauthentication Attacks

Among the more frequent attacks we might witness or detect is a deauthentication/dissociation attack. This is a commonplace link-layer precursor attack that adversaries might employ for several reasons:

1. `To capture the WPA handshake to perform an offline dictionary attack`
2. `To cause general denial of service conditions`
3. `To enforce users to disconnect from our network, and potentially join their network to retrieve information`

In essence, the attacker will fabricate an 802.11 deauthentication frame pretending it originates from our legitimate access point. By doing so, the attacker might manage to disconnect one of our clients from the network. Often, the client will reconnect and go through the handshake process while the attacker is sniffing.

![[deauth-attack.webp]]

The client device cannot really discern the difference without additional controls like IEEE 802.11w (Management Frame Protection). Each deauthentication request is associated with a reason code explaining why the client is being disconnected.

In most scenarios, basic tools like `aireplay-ng` and `mdk4` employ reason `code 7` for deauthentication.

### Identifying Deauthentication Attacks