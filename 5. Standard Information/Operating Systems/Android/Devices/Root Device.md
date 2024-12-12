1. [[Flash Standard Images]] with a `user-debug` variant which will give you `su`
2. Magisk

## Magisk

Download the build release required from: [Full OTA Images for Nexus and Pixel Devices  |  Google Play services  |  Google for Developers](https://developers.google.com/android/ota)

1. Extract the `boot.img`. Some images have the `boot.img` available. Otherwise use [[Extract Android OTA Payload]]
2. Push `boot.img` to device: `adb push boot.img /sdcard/Download`
3. Install Magisk from: [Magisk v28.1](https://github.com/topjohnwu/Magisk/releases/tag/v28.1)
4. Install Magisk to the device: `adb install Magisk.apk`
5. Open the Magisk app 
6. Click the install button and then `Select and patch a file` option
7. Select the `boot.img` in the download folder
8. Click `Lets go`
9. Extract the patched `boot.img` from the Sdcard directory as seen on the device: `adb pull xxx`
10. Run `adb reboot bootloader`
11. Run `fastboot flash boot patched_boot.img`
12. Restart the device.
13. Open the Magisk app and within adb shell then run `su`
14. Accept any popups on the device



#### Root Emulator

Android Studio:

1. Tools -> Device Manager
2. Create a new AVD
3. Start emulator through command line
4. See [[RootAVD]]
