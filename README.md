# TWRP device tree for Y700 gen4 TB322FC

TWRP build for Legion Tablet Y700 gen4.

## Other devices
- [TWRP for Y700 2023 (gen2)](https://github.com/polygraphene/android_device_lenovo_TB320FC)
- [TWRP for Y700 2025 (gen3)](https://github.com/polygraphene/android_device_lenovo_TB321FU)

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

If there is no error, recovery.img will be found in `out/target/product/TB322FC/recovery.img`

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

Download from recovery image from [release](https://github.com/polygraphene/android_device_lenovo_TB322FC/releases) and flash it.

For locked device:  
Devices with the ZUI 1.5.10.138 or prior can be flashed without unlocking (Lenovo testkey vulnerability).
Use EDL mode to flash because fastboot flash doesn't work on locked device.

### Flash with qdlrs
To flash with Qualcomm's [qdlrs](https://github.com/qualcomm/qdlrs):

1. Download [my build](https://github.com/polygraphene/qdlrs/releases) of qdlrs.
2. Get xbl_s_devprg_ns.melf from qpst ROM.
3. Check COM<number> in device manager and run the following commands:
```
> .\qdl-rs-windows-x64.exe --loader-path xbl_s_devprg_ns.melf --storage-type ufs --backend serial --dev-path COM<number> --phys-part-idx 4 write recovery_a TWRP-3.7.1-16-TB322FC-2026-04-04-2-portrait.img
...
Loader sent. Hack away!
Found protocol version 1
Sending partition recovery_a: 100.00 MB / 100.00 MB [=================================================================================] 100.00 % 40.06 MB/s A
ll went well! Resetting to edl

> .\qdl-rs-windows-x64.exe --loader-path xbl_s_devprg_ns.melf --storage-type ufs --backend serial --dev-path COM<number> --phys-part-idx 4 write recovery_b TWRP-3.7.1-16-TB322FC-2026-04-04-2-portrait.img
...
> .\qdl-rs-windows-x64.exe --loader-path xbl_s_devprg_ns.melf --storage-type ufs --backend serial --dev-path COM<number> reset
...
```

### Flash via fastboot
For unlocked device:

```shell
fastboot flash recovery recovery.img
```

or

```shell
fastboot flash recovery_a recovery.img
fastboot flash recovery_b recovery.img
```

## Acknowledgment

- [TWRP-Test](https://github.com/TWRP-Test/platform_manifest_twrp_aosp)
- [twrp_device_oplus_sm87xx](https://github.com/kmiit/twrp_device_oplus_sm87xx) - This repo is base on it.
- [twrp_device_xiaomi_sm8750_thales](https://github.com/YuKongA/twrp_device_xiaomi_sm8750_thales)
- [TWRP](https://twrp.me/)
- [qdlrs](https://github.com/qualcomm/qdlrs)

