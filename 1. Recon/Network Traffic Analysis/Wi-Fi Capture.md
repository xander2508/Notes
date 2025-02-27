---
tags:
  - Recon
  - NetworkTrafficAnalysis
---
Let's assume we do possess a Wi-Fi interface capable of monitor mode. We could enumerate our wireless interfaces in Linux using the following command:

```shell-session
iwconfig
```

1. We have a couple of options to set our interface into monitor mode. Firstly, employing `airodump-ng`, we can use the ensuing command:

```shell-session
sudo airmon-ng start wlan0
```

2. Secondly, using system utilities, we would need to deactivate our interface, modify its mode, and then reactivate it.

```shell-session
sudo ifconfig wlan0 down
```
```shell-session
sudo iwconfig wlan0 mode monitor
```
```shell-session
sudo ifconfig wlan0 up
```

We could verify if our interface is in `monitor mode` using the `iwconfig` utility.

```shell-session
$ iwconfig

wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.457 GHz  Tx-Power=20 dBm   
          Retry short  long limit:2   RTS thr:off   Fragment thr:off
          Power Management:off
```

To commence capturing traffic from our clients and network, we can employ `airodump-ng`. We need to specify our AP's channel with `-c`, its BSSID with `--bssid`, and the output file name with `-w`.

```shell-session
sudo airodump-ng -c 4 --bssid F8:14:FE:4D:E6:F1 wlan0 -w raw
```

We can use `tcpdump` to achieve similar outcomes, but Airodump-ng proves equally effective.