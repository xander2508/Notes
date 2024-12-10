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
