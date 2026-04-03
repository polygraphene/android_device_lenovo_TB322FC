# TWRP device tree for Y700 gen4 TB322FC

## Build it yourself?

```shell
mkdir twrp && cd twrp
repo init --depth=1 -u https://github.com/TWRP-Test/platform_manifest_twrp_aosp.git -b twrp-16.0
repo sync
(cd bootable/recovery; git fetch https://github.com/polygraphene/android_bootable_recovery twrp-16.0-TB322FC && git checkout FETCH_HEAD)
git clone --depth=1 https://github.com/polygraphene/android_device_lenovo_TB322FC device/lenovo/TB322FC
```

```shell
source build/envsetup.sh
lunch twrp_TB322FC
make recoveryimage
```

If there is no error, recovery.img will be found in `out/target/product/sm87xx/recovery.img`

## Features

Works:

- [X] ADB
- [X] Display
- [X] Decryption
- [X] Fasbootd
- [X] Flashing
- [X] MTP
- [X] Touch
- [X] USB OTG
- [X] Vibrator

## To use it:

For locked device:
Devices with the ZUI version below or equal to 1.5.10.138 can be flashed without unlocking (Lenovo testkey vulnerability).
Use [qualcomm/qdl](https://github.com/qualcomm/qdlrs) or [bkerler/edl](https://github.com/bkerler/edl) to flash the image by EDL mode.
TODO: Add detailed instruction later.

For unlocked device:

```shell
fastboot flash recovery recovery.img
```

or

```shell
fastboot flash recovery_a recovery.img
fastboot flash recovery_b recovery.img
```
