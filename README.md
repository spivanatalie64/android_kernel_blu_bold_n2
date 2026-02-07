# Kernel for BLU Bold N2

## Device Information

- **Device**: BLU Bold N2
- **Codename**: bold_n2
- **SoC**: MediaTek Dimensity 810 (MT6833)
- **Kernel Version**: Linux 4.14.186
- **Architecture**: ARM64

## Current Status

This repository contains kernel configuration and documentation for building the kernel.

Currently, the device tree uses a **prebuilt kernel** extracted from stock firmware located at:
`device/blu/bold_n2/prebuilt-kernel/`

## Prebuilt Kernel Information

**Source**: Extracted from stock firmware BOLD_N0050UU_V11.0.04.04_GENERIC_20220914_2257

- **Image.gz**: Compressed kernel image (~13MB)
- **dtb.img**: Device Tree Blob
- **dtbo.img**: Device Tree Blob Overlay

### Kernel Build Information
- Version: Linux 4.14.186
- Build Date: September 2022
- Compiler: Unknown (extracted binary)
- Config: Not embedded (IKCONFIG not enabled)

## Building from Source

To build the kernel from source, you'll need:

### 1. Obtain Kernel Source

Option A: Extract from vmlinux (if available)
```bash
# Decompile vmlinux to get source hints
# This requires significant reverse engineering
```

Option B: Use MediaTek kernel source
```bash
# MediaTek may provide kernel source
# Check MediaTek developer portal
```

### 2. Kernel Configuration

A placeholder defconfig has been created at:
`arch/arm64/configs/bold_n2_defconfig`

This is a starting point and needs to be populated with actual configuration.

### 3. Build Instructions

Once you have the kernel source:

```bash
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-android-
export SUBARCH=arm64

# Configure
make bold_n2_defconfig

# Build
make -j$(nproc) Image.gz
make -j$(nproc) dtbs
make -j$(nproc) dtbo.img

# Output will be:
# arch/arm64/boot/Image.gz
# arch/arm64/boot/dts/mediatek/*.dtb
```

### 4. Update Device Tree

After building, update the device tree BoardConfig.mk:

```makefile
# Replace prebuilt kernel with source build
TARGET_KERNEL_SOURCE := kernel/blu/bold_n2
TARGET_KERNEL_CONFIG := bold_n2_defconfig
BOARD_KERNEL_IMAGE_NAME := Image.gz

# Remove these lines:
# TARGET_PREBUILT_KERNEL := $(LOCAL_PATH)/prebuilt-kernel/Image.gz
# TARGET_PREBUILT_DTB := $(LOCAL_PATH)/prebuilt-kernel/dtb.img
```

## Kernel Features

Based on MediaTek MT6833 platform:

- **CPU**: Octa-core (2x Cortex-A76 @ 2.4GHz + 6x Cortex-A55 @ 2.0GHz)
- **GPU**: Mali-G57 MC2
- **Memory**: LPDDR4X
- **Storage**: UFS 2.1/2.2
- **Display**: MIPI DSI
- **Camera**: ISP with dual camera support
- **Connectivity**: 5G modem, WiFi 6, Bluetooth 5.1
- **Audio**: MediaTek audio codec

## MediaTek-Specific Drivers

Required drivers for MT6833:

- `drivers/misc/mediatek/` - MediaTek platform drivers
- Camera ISP drivers
- GPU drivers (Mali)
- Display drivers
- Audio codec drivers
- Thermal management
- Power management (CPUFREQ, CPUIDLE)
- Connectivity (WiFi, Bluetooth, GPS)
- Sensors

## Kernel Patches

Any device-specific patches should be documented here:

1. **Boot optimization patches**
2. **Hardware enablement patches**
3. **Performance tuning patches**
4. **Security patches**

## Known Issues

- Config extraction from prebuilt kernel failed (no IKCONFIG)
- Kernel source not yet obtained
- Building from source requires MediaTek kernel tree

## References

- [MediaTek Developer Resources](https://online.mediatek.com/)
- [Linux Kernel Documentation](https://www.kernel.org/doc/)
- [ARM64 Kernel Building](https://www.kernel.org/doc/html/latest/arm64/index.html)

## License

The Linux kernel is licensed under GPL v2.

## Contributing

Contributions welcome! Please:

1. Document all changes
2. Test on actual hardware
3. Submit patches via pull request

## Support

For kernel-related issues:
- Check device tree documentation
- Review kernel logs: `dmesg`
- Check boot logs: `adb shell dmesg | grep kernel`

---

**Note**: This is a work in progress. Contributions to extract kernel config and build from source are welcome!
