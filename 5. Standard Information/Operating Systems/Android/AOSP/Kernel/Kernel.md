## Install

[Build kernels  |  Android Open Source Project](https://source.android.com/docs/setup/build/building-kernels)

```
sudo apt-get update
```

```
mkdir ~/.bin
```

```
PATH=~/.bin:$PATH
```

```
export REPO=$(mktemp /tmp/repo.XXXXXXXXX)
curl -o ${REPO} https://storage.googleapis.com/git-repo-downloads/repo
gpg --recv-keys 8BB9AD793E8E6153AF0F9A4416530D5E920F5C65
curl -s https://storage.googleapis.com/git-repo-downloads/repo.asc | gpg --verify - ${REPO} && install -m 755 ${REPO} ~/.bin/repo
```

```
repo version
```

Replace `main` with a specific tag: [Kernel branches and their build systems  |  Android Open Source Project](https://source.android.com/docs/setup/reference/bazel-support)

```
repo init -u https://android.googlesource.com/kernel/manifest -b BRANCH
```

```
repo sync -c -j8 --no-tag
```

## Build

Locate the device specific build settings at the bottom of the build sh file. 
Navigate to the found folder: e.g. `/privte/devices/google/shusky`

Within the `*.fragment` file add the following two lines:

For debug symbols:
```
CONFIG_DEBUG_INFO=y
```

For debug information and better bpf tooling:
```
CONFIG_DEBUG_INFO_BTF=y
```

Back in the root directory where `shusky` is the Android device codename:

```
BUILD_AOSP_KERNEL=1 ./build_shusky.sh
```

## Usage

[Build Pixel kernels  |  Android Open Source Project](https://source.android.com/docs/setup/build/building-pixel-kernels#flash_the_kernel_images)

> [!NOTE]
>  **Note:** If you haven't disabled verification, you need to do it before flashing the custom kernel. Here is the command to do so:
>  
> ```
> fastboot oem disable-verification
> ```


To flash the kernel images, run the `fastboot flash` command for each kernel partition listed for your device. For dynamic partitions, you need to reboot into `fastbootd` mode before flashing.

| Device                                                                                                                                                                | Kernel Partitions                                                                                                    |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Pixel 6 (oriole)  <br>Pixel 6 Pro (raven)  <br>Pixel 6a (bluejay)                                                                                                     | boot  <br>dtbo  <br>vendor_boot  <br>vendor_dlkm _(dynamic partition)_                                               |
| Pixel 8 (shiba)  <br>Pixel 8 Pro (husky)  <br>Pixel Fold (felix)  <br>Pixel Tablet (tangorpro)  <br>Pixel 7a (lynx)  <br>Pixel 7 (panther)  <br>Pixel 7 Pro (cheetah) | boot  <br>dtbo  <br>vendor_kernel_boot  <br>vendor_dlkm _(dynamic partition)_  <br>system_dlkm _(dynamic partition)_ |

Here are the flashing commands for Pixel 6 on `android-mainline`:

```
fastboot flash boot        out/slider/dist/boot.img
fastboot flash dtbo        out/slider/dist/dtbo.img
fastboot flash vendor_boot out/slider/dist/vendor_boot.img
fastboot reboot fastboot
fastboot flash vendor_dlkm out/slider/dist/vendor_dlkm.img
```

The kernel images can be found in the DIST_DIR.

|Kernel branch|DIST_DIR|
|---|---|
|v5.10|`out/mixed/dist`|
|v5.15 and later|`out/DEVICE/dist`|