## Install

[Set up for AOSP development (9.0 or later)  |  Android Open Source Project](https://source.android.com/docs/setup/start/requirements)

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

Replace `main` with a specific tag: [Codenames, tags, and build numbers  |  Android Open Source Project](https://source.android.com/docs/setup/reference/build-numbers#source-code-tags-and-builds)

```
repo init --partial-clone -b main -u https://android.googlesource.com/platform/manifest
```

```
repo sync -c -j8
```

## Build

```
source build/envsetup.sh
```

Before building Android, you must identify a _target_ to build. A target reflects the target platform you're building for. To identify your target to build, use the `lunch` command followed by a string representing the target.  [Build Android  |  Android Open Source Project](https://source.android.com/docs/setup/build/building) For example:

```
lunch aosp_cf_x86_64_phone-trunk_staging-userdebug
```

```
lunch product_name-release_config-build_variant
```

```
m
```

## Export

Output an emulator zip file

```
make emu_img_zip -j8
```

## Build to Emulator

Copy the emulator zip to the emulator `system-images` file and extract the folder. 