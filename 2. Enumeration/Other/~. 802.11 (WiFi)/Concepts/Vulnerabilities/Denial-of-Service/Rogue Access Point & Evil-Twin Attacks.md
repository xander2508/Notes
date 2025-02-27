---
tags:
  - Enumeration
  - Misc
  - 802-11
  - Concepts
  - Vulnerabilities
  - Denial-of-Service
  - WiFi
---
Addressing rogue access points and evil-twin attacks can seem like a gargantuan task due to their often elusive nature. Nevertheless, with the appropriate strategies in place, these illegitimate access points can be detected and managed effectively.

## Rogue Access Point

A Rogue Access Point (RAP) is a wireless access point that has been installed on a network without authorization. These devices are often used by attackers to intercept sensitive information, such as login credentials or financial data, from unsuspecting users who connect to them. Rogue Access Points can be set up by physically connecting a device to the network or by using software to create a virtual access point.

A rogue access point primarily serves as a tool to circumvent perimeter controls in place. An adversary might install such an access point to sidestep network controls and segmentation barriers, which could, in many cases, take the form of hotspots or tethered connections. These rogue points have even been known to infiltrate air-gapped networks. Their primary function is to provide unauthorized access to restricted sections of a network. The critical point to remember here is that rogue access points are directly connected to the network.
#### Finding Rogue Access Points

On the other hand, detecting rogue access points can often be a simple task of checking our network device lists. In the case of hotspot-based rogue access points (such as Windows hotspots), we might scrutinize wireless networks in our immediate vicinity. If we encounter an unrecognizable wireless network with a strong signal, particularly if it lacks encryption, this could indicate that a user has established a rogue access point to navigate around our perimeter controls.
## Evil-Twin

An Evil-Twin router is a type of rogue access point that is set up to mimic a legitimate Wi-Fi network in order to trick users into connecting to it. This allows attackers to intercept sensitive information such as usernames, passwords, and credit card numbers.

An Evil-Twin attack is a type of wireless attack where an attacker creates a fake wireless network that looks like a legitimate one, in order to trick users into connecting to it. Once connected, the attacker can intercept any data being transmitted over the network, including sensitive information like passwords and credit card numbers. This type of attack is often carried out in public places, such as coffee shops or airports, where people are more likely to connect to open Wi-Fi networks without verifying their legitimacy.

### Detection 

We could utilize the ESSID filter for Airodump-ng to detect Evil-Twin style access points.

```shell-session
sudo airodump-ng -c 4 --essid HTB-Wireless wlan0 -w raw

CH  4 ][ Elapsed: 1 min ][ 2023-07-13 16:06    
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH   MB   ENC CIPHER  AUTH ESSID
 F8:14:FE:4D:E6:F2   -7 100      470      155    0   4   54   OPN              HTB-Wireless
 F8:14:FE:4D:E6:F1   -5  96      682        0    0   4  324   WPA2 CCMP   PSK  HTB-Wireless 
```

The above example would show that in fact an attacker might have spun up an open access point that has an identical ESSID as our access point. An attacker might do this to host what is commonly referred to as a [[Hostile Portal Attacks]]. A hostile portal attack is used by attackers in order extract credentials from users among other nefarious actions.

We might also want to be vigilant about [[Deauthentication Attacks]] attempts, which could suggest enforcement measures from the attacker operating the evil-twin access point.

To conclusively ascertain whether this is an anomaly or an Airodump-ng error, we can commence our traffic analysis efforts. To filter for beacon frames, we could use the following within [[Wireshark]].

```
(wlan.fc.type == 00) and (wlan.fc.type_subtype == 8)
```

Beacon analysis is crucial in differentiating between genuine and fraudulent access points. One of the initial places to start is the `Robust Security Network (RSN)` information. This data communicates valuable information to clients about the supported ciphers, among other things.

Our legitimate access point's RSN information.

![[2-evil-twin.webp]]

When we switch to the illegitimate access point's RSN information, we may find it conspicuously missing.

![[3-evil-twin.webp]]

We should always probe additional fields for discrepancies, particularly when dealing with more sophisticated evil-twin attacks. For example, an attacker might employ the same cipher that our access point uses, making the detection of this attack more challenging.

Under such circumstances, we could explore other aspects of the beacon frame, such as vendor-specific information, which is likely absent from the attacker's access point.

#### Identifying a Fallen User

Despite comprehensive security awareness training, some users may fall prey to attacks like these. Fortunately, in the case of open network style evil-twin attacks, we can view most higher-level traffic in an unencrypted format.

If we detect ARP requests emanating from a client device connected to the suspicious network, we would identify this as a potential compromise indicator. In such instances, we should record pertinent details about the client device to further our incident response efforts.

1. `Its MAC address`
2. `Its host name`

Consequently, we might be able to instigate password resets and other reactive measures to prevent further infringement of our environment.