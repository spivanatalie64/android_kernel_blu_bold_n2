# Kernel for BLU Bold N2

This repository contains the kernel configuration and documentation for the BLU Bold N2 (bold_n2) device running LineageOS.

## Device Information

- **Device**: BLU Bold N2
- **Codename**: bold_n2
- **SoC**: MediaTek Dimensity 810 (MT6833)
- **Architecture**: ARM64 (aarch64)
- **Kernel Version**: Linux 4.14.186
- **Build Date**: Sep 14 2022

## Current Status: Prebuilt Kernel

The device currently uses a **prebuilt kernel** extracted from stock firmware located in the device tree:

```
device/blu/bold_n2/prebuilt-kernel/
├── Image.gz      # Compressed kernel image
├── dtb.img       # Device tree blob
└── dtbo.img      # Device tree overlay
```

## Kernel Configuration

The **actual kernel configuration has been successfully extracted** from the stock firmware's vmlinux and is available at:

```
arch/arm64/configs/bold_n2_defconfig
```

This is the **complete, real configuration** (5512 lines) used to build the stock kernel, extracted using the `extract-ikconfig` tool from the unstripped vmlinux binary.

### Key Configuration Highlights

- **Platform**: `CONFIG_MACH_MT6833=y`
- **MTK Platform ID**: `CONFIG_MTK_PLATFORM="mt6853"` (kernel platform name)
- **Project**: `CONFIG_ARCH_MTK_PROJECT="k6833v1_64"`
- **Compiler**: Android clang 11.0.1
- **Cross Compile**: `aarch64-linux-android-`

### MediaTek-Specific Features Enabled

- MTK CPU frequency scaling
- MTK power management (PTPOD, CPU_MSSV, SLBC)
- MTK thermal management
- MTK QoS framework v2
- MT6359P PMIC support
- MT6360 PMU (charger, power management)
- MTK display (DRM_MEDIATEK)
- MTK audio (SND_SOC_MT6833)
- MTK video codec (VCODEC, JPEG, VCU)
- MTK security (DEVAPC, DEVMPU)
- MTK low power modes

## Building from Source (Future)

### Prerequisites

```bash
# Install toolchain
sudo apt install gcc-aarch64-linux-gnu build-essential bc bison flex libssl-dev
```

### When Kernel Source Becomes Available

```bash
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-gnu-
export SUBARCH=arm64

# Use extracted config
make bold_n2_defconfig

# Build
make -j$(nproc) Image.gz
make -j$(nproc) dtbs
make -j$(nproc) modules
```

### Output Files

- `arch/arm64/boot/Image.gz` - Kernel image
- `arch/arm64/boot/dts/mediatek/mt6833-*.dtb` - Device tree
- Modules in various subdirectories

## Kernel Command Line

From boot.img:

```
console=tty0 console=ttyMT3,921600n1 root=/dev/ram 
vmalloc=496M slub_max_order=0 slub_debug=O 
bootopt=64S3,32N2,64N2 buildvariant=user
```

## Kernel Build Information

Extracted from vmlinux:

```
Linux version 4.14.186 (nobody@android-build)
(Android (6443078 based on r383902) clang version 11.0.1)
#2 SMP PREEMPT Wed Sep 14 22:57:41 CST 2022
```

## Boot Image Parameters

From unpacking boot.img:

- **Base Address**: 0x40078000
- **Page Size**: 2048 bytes
- **Header Version**: 2
- **OS Version**: 11.0.0
- **OS Patch Level**: 2022-09
- **DTB Included**: Yes (dtb.img)
- **DTBO Included**: Yes (dtbo.img)

## MediaTek Platform Notes

The MT6833 (Dimensity 810) uses:

- **CPU**: 2x Cortex-A76 @ 2.4GHz + 6x Cortex-A55 @ 2.0GHz
- **GPU**: Mali-G57 MC2
- **Kernel Platform**: Shares platform code with MT6853 family
- **PMIC**: MT6359P (power management IC)
- **PMU**: MT6360 (battery/charging)

## Directory Structure

```
.
├── README.md                          # This file
├── BUILDING.md                        # Detailed build guide
├── arch/arm64/configs/
│   └── bold_n2_defconfig             # Real extracted kernel config (5512 lines)
└── kernel_config_work/               # Config extraction documentation
    ├── kernel_version.txt            # Kernel version info
    ├── extraction_log.txt            # Extraction process log
    └── config_candidates.txt         # Config hints
```

## Future Development

### Short Term
- Document all MediaTek-specific config options
- Create optimized defconfig variants (debug, performance, battery)
- Test kernel building when source becomes available

### Long Term
- Obtain MediaTek MT6833 kernel source
- Update to newer kernel version (5.x or 6.x)
- Implement custom patches for LineageOS optimization
- Mainline device tree improvements

## License

The Linux kernel is released under the GNU GPL v2.

## References

- [Linux Kernel](https://www.kernel.org/)
- [ARM64 Boot Protocol](https://www.kernel.org/doc/html/latest/arm64/booting.html)
- [MediaTek Platform Documentation](https://online.mediatek.com/)
- [Android Kernel Building](https://source.android.com/docs/setup/build/building-kernels)

## Credits

- Kernel configuration extracted from BLU Bold N2 stock firmware
- Device tree and build system: LineageOS contributors
- MediaTek platform support: MediaTek

---

**Note**: This kernel repository contains the complete, production kernel configuration extracted from the stock firmware. While we currently use a prebuilt kernel, this configuration enables future source-based kernel building when MediaTek source code becomes available.
