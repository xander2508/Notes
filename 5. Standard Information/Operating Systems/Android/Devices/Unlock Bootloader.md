
Ensure [[Android Debug Bridge (ADB)|ADB]] and [[Fastboot]] are installed. Enable USB debugging, see [[Android Debug Bridge (ADB)#Enable adb debugging on your device]]

Connect the device to the computer.

Run the following commands:

```
adb reboot bootloader
```

Watch for interaction on the device to confirm flashing unlock:

```
fastboot flashing unlock
```

```
fastboot flashing unlock_critical
```