# Building the Kernel

## Current Status

The BLU Bold N2 currently uses a **prebuilt kernel** from stock firmware.

This repository provides:
- Documentation for kernel building
- Placeholder defconfig
- Build instructions for future source builds

## Prebuilt Kernel Location

The prebuilt kernel is in the device tree:
```
device/blu/bold_n2/prebuilt-kernel/
├── Image.gz      # Kernel image
├── dtb.img       # Device tree blob
└── dtbo.img      # Device tree overlay
```

## Future: Building from Source

### Prerequisites

```bash
# Install build tools
sudo apt install build-essential bc bison flex libssl-dev

# Install cross-compiler
sudo apt install gcc-aarch64-linux-gnu
```

### Obtaining Kernel Source

**Option 1**: MediaTek Kernel Source
- Check MediaTek developer portal for MT6833 kernel source
- May require NDA or developer agreement

**Option 2**: Reverse Engineering
- Extract symbols from vmlinux
- Requires significant effort and expertise

### Build Commands (when source available)

```bash
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-gnu-
export SUBARCH=arm64

# Clean
make mrproper

# Configure
make bold_n2_defconfig

# Or use extracted config
# cp extracted_config .config
# make olddefconfig

# Build kernel
make -j$(nproc) Image.gz

# Build device tree
make -j$(nproc) dtbs

# Build modules
make -j$(nproc) modules

# Output files:
# arch/arm64/boot/Image.gz
# arch/arm64/boot/dts/mediatek/mt6833-*.dtb
```

### Testing

```bash
# Flash kernel via fastboot
fastboot flash boot boot.img

# Or via LineageOS build system
# Place kernel in device tree and rebuild
```

## Kernel Configuration Needs

When building from source, ensure these are enabled:

- MediaTek platform drivers
- MT6833 SoC support
- Display (MIPI DSI)
- Camera (ISP)
- WiFi/Bluetooth
- 5G modem
- Sensors
- GPU (Mali-G57)
- Audio codec

## References

- [Kernel Building Guide](https://www.kernel.org/doc/html/latest/admin-guide/README.html)
- [ARM64 Boot](https://www.kernel.org/doc/html/latest/arm64/booting.html)
- [MediaTek Platform](https://online.mediatek.com/)

