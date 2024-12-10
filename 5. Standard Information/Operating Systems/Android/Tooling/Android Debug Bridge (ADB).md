---
tags:
  - Tooling
aliases:
  - ADB
---

[Android Debug Bridge (adb)  |  Android Studio  |  Android Developers](https://developer.android.com/tools/adb)
[ADB(1) MAN PAGE](https://android.googlesource.com/platform/packages/modules/adb/+/refs/heads/master/docs/user/adb.1.md)

Android Debug Bridge (`adb`) is a versatile command-line tool that lets you communicate with a device. The `adb` command facilitates a variety of device actions, such as installing and debugging apps. `adb` provides access to a Unix shell that you can use to run a variety of commands on a device. It is a client-server program that includes three components:

- **A client**, which sends commands. The client runs on your development machine. You can invoke a client from a command-line terminal by issuing an `adb` command.
- **A daemon (adbd)**, which runs commands on a device. The daemon runs as a background process **on each device**.
- **A server**, which manages communication between the client and the daemon. The server runs as a background process on your development machine.

Adb can function over Wi-Fi or a physical connection.

## Install

[SDK Platform Tools release notes  |  Android Studio  |  Android Developers](https://developer.android.com/tools/releases/platform-tools)

Ensure the downloaded binaries are add to path

## Enable adb debugging on your device

To use adb with a device connected over USB, you must enable **USB debugging** in the device system settings, under **Developer options**.

1. On your device, find the **Build number** option. The following table shows the settings location of the **Build number** on various devices:

|Device | Setting |
|---|---|
|Google Pixel|**Settings** > **About phone** > **Build number**|
|Samsung Galaxy S8 and later|**Settings** > **About phone** > **Software information** > **Build number**|
|LG G6 and later|**Settings** > **About phone** > **Software info** > **Build number**|
|HTC U11 and later|**Settings** > **About** > **Software information** > **More** > **Build number** _or_ **Settings** > **System** > **About phone** > **Software information** > **More** > **Build number**|
|OnePlus 5T and later|**Settings** > **About phone** > **Build number**|

2. Tap the **Build Number** option seven times until you see the message `You are now a developer!` This enables developer options on your device.
3. Return to the previous screen to find **Developer options** at the bottom.

Enable **USB debugging** in the device system settings under **Developer options**. You can find this option in one of the following locations, depending on your Android version:

- Android 9 (API level 28) and higher: **Settings > System > Advanced > Developer Options > USB debugging**
- Android 8.0.0 (API level 26) and Android 8.1.0 (API level 27): **Settings > System > Developer Options > USB debugging**
- Android 7.1 (API level 25) and lower: **Settings > Developer Options > USB debugging**

## Command Options

#### Query for devices  

```
adb devices -l
```

In response, `adb` prints this status information for each device:

- **Serial number:** `adb` creates a string to uniquely identify the device by its port number. Here's an example serial number: `emulator-5554`
- **State:** The connection state of the device can be one of the following:
    - `offline`: The device is not connected to `adb` or is not responding.
    - `device`: The device is connected to the `adb` server. Note that this state does not imply that the Android system is fully booted and operational, because the device connects to `adb` while the system is still booting. After boot-up, this is the normal operational state of a device.
    - `no device`: There is no device connected.
- **Description:** If you include the `-l` option, the `devices` command tells you what the device is. This information is helpful when you have multiple devices connected so that you can tell them apart.
#### Issue shell commands

You can use the `shell` command to issue device commands through `adb` or to start an interactive shell. To issue a single command, use the `shell` command like this:

```
adb [-d |-e | -s serial_number] shell shell_command
```

```
adb [-d | -e | -s serial_number] shell
```

```
adb shell ls /system/bin
```


#### Logcat command-line tool

[Logcat command-line tool  |  Android Studio  |  Android Developers](https://developer.android.com/tools/logcat)

Logcat is a command-line tool that dumps a log of system messages including messages that you have written from your app with the [Log](https://developer.android.com/reference/android/util/Log) class.

```
[adb] shell logcat [<option>] ... [<filter-spec>] ...
```

```
adb logcat --help
```

The following is an example of a filter expression that suppresses all log messages except those with the tag "ActivityManager" at priority "Info" or above and those with the tag "MyApp" with priority "Debug" or above:

```
adb logcat ActivityManager:I MyApp:D *:S
```

The following filter expression displays all log messages with priority level "warning" and higher on all tags:

```
adb logcat *:W
```

#### Install an app

You can use `adb` to install an APK on an emulator or connected device with the `install` command:

```
adb install path_to_apk
```

**-r**:     Replace existing application.
**-g**:     Grant all runtime permissions.
**-t**:     Allow test packages.

##### Install split APKs

```
adb install-multiple -r -t base.apk split_config.arm64_v8a.apk split_config.xxhdpi.apk
```


#### Copy files to and from a device

Use the `pull` and `push` commands to copy files to and from a device. Unlike the `install` command, which only copies an APK file to a specific location, the `pull` and `push` commands let you copy arbitrary directories and files to any location in a device.

To copy a file or directory and its sub-directories _from_ the device, do the following:

```
adb pull remote local
```

To copy a file or directory and its sub-directories _to_ the device, do the following:

```
adb push local remote
```

Replace `local` and `remote` with the paths to the target files/directory on your development machine (local) and on the device (remote). For example:

```
adb push myfile.txt /sdcard/myfile.txt
```

#### List installed packages

```
adb shell pm list packages
```

**-3**: List only user installed packages

To list the path of the package located:

```
adb shell pm path <PACKAGE_ID>
```
