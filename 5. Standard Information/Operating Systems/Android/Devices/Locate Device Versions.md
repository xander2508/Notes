
Version syntax:

```
TQ1A.221205.011
```

TQ1A: Android Version Code 1st Quarter
22        : Year 2022
12: Dec
05: 5th

| Code | Meaning                          |
| ---- | -------------------------------- |
| TQ1A | Android Version Code 1st Quarter |
| 22   | Year 2022                        |
| 12   | December                         |
| 05   | 5th                              |
| 011  | Version Number                   |



Use an ADB command to get the device version:

```
adb shell getprop ro.product.build.fingerprint
```

OTA versions and their code names:
[Full OTA Images for Nexus and Pixel Devices  |  Google Play services  |  Google for Developers](https://developers.google.com/android/ota)