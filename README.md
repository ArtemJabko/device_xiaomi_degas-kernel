# Prebuilt kernel for Xiaomi 14T (degas)

Prebuilt GKI kernel (MediaTek MT6897 / Dimensity 8300-Ultra) for the LineageOS
build of the Xiaomi 14T (codename `degas`).

## Contents

| Artifact              | Description                                       |
| :-------------------- | :------------------------------------------------ |
| `Image.lz4`           | GKI kernel image (LZ4 compressed), from stock firmware |
| `dtb/mt6897.dtb`      | Device tree blob for the MT6897 platform          |
| `dtbo.img`            | Device tree overlay image (degas)                 |
| `modules/*.ko`        | Kernel modules (vendor_dlkm / vendor_ramdisk)     |
| `kernel-uapi-headers.tar.gz` | Kernel UAPI headers for building in-tree HALs |

## Sources

The artefacts were extracted from an official Xiaomi degas firmware dump:

* `Image.lz4` - unpacked from the stock `boot.img`
* `dtb/mt6897.dtb` - unpacked from the stock `vendor_boot.img`
* `dtbo.img` - stock `dtbo.img` partition
* `modules/*.ko` - unpacked from the stock `vendor_boot` ramdisk (`vendor_dlkm`)

The generic MT6897 module set mirrors that used by the sister `duchamp` (POCO X6 Pro)
device tree, plus the degas-specific display panels (`panel-n12a-*`) and touch drivers
(`*_rothko`, `xiaomi_touch_common`).

## Usage in LineageOS

Referenced from `device/xiaomi/degas/BoardConfig.mk` via:

```
KERNEL_PATH := $(DEVICE_PATH)-kernel
TARGET_PREBUILT_KERNEL := $(KERNEL_PATH)/Image.lz4
```

## Notes

* The degas device tree (`device_xiaomi_degas`) is a port of the
  `mt6897-devs/device_xiaomi_duchamp` tree; see `DIFFERENCES.md` there.
* `vendor_dlkm.modules.load` / `vendor_ramdisk.modules.load` lists are kept in
  the device tree and must match the module names shipped here.
