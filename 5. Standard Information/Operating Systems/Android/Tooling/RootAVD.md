
[newbit / rootAVD · GitLab](https://gitlab.com/newbit/rootAVD)

## Install

```
git clone https://gitlab.com/newbit/rootAVD
```

## Usage

Ensure an emulator is running:

```
./rootAVD.sh ListAllAVDs | grep CHOSEN_AVD
```

Copy the path outputted, then run:

```
./rootAVD.sh OUTPUTTED_PATH
```

Do not save the state if it asks you too.

1. Reboot Emulator with the same command.
2. Open Magisk
3. Click the `update` button
4. Open Magisk again
5. Click `Ok` for `Requires additional setup`
6. Click `Direct Install` then `Lets go`

Emulator is now root