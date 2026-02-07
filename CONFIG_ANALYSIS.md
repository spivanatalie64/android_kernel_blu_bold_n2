# BLU Bold N2 Kernel Configuration Analysis

**Extracted from**: Stock firmware vmlinux  
**Total config lines**: 5,512  
**Kernel version**: Linux 4.14.186  
**Platform**: MediaTek MT6833 (Dimensity 810)

## Configuration Source

The kernel configuration was extracted from the unstripped vmlinux ELF binary found in the stock firmware using the `extract-ikconfig` script. This is the **actual production configuration** used by BLU for the Bold N2.

```bash
file: ELF 64-bit LSB shared object, ARM aarch64, version 1 (SYSV), 
      statically linked, with debug_info, not stripped
size: 619 MB (unstripped with debug symbols)
```

## Platform Configuration

### MediaTek Platform Settings

```
CONFIG_MACH_MT6833=y                          # MT6833 SoC support
CONFIG_MTK_PLATFORM="mt6853"                  # Platform family name
CONFIG_ARCH_MTK_PROJECT="k6833v1_64"          # Project codename
CONFIG_BUILD_ARM64_APPENDED_DTB_IMAGE_NAMES="mediatek/mt6833"
```

**Note**: MT6833 uses the MT6853 platform code base (MediaTek platform family).

### CPU Architecture

```
CONFIG_ARM64=y                                # ARM 64-bit
CONFIG_64BIT=y
CONFIG_SMP=y                                  # Symmetric multiprocessing
CONFIG_NR_CPUS=8                              # 8 CPU cores
CONFIG_SCHED_MC=y                             # Multi-core scheduling
CONFIG_ARM64_PAGE_SHIFT=12                    # 4KB pages
CONFIG_PGTABLE_LEVELS=3                       # 3-level page tables
```

### Compiler & Toolchain

```
CONFIG_CROSS_COMPILE="aarch64-linux-android-"
# Built with: Android clang 11.0.1 (r383902)
# Linker: LLD 11.0.1
```

## Key Subsystems

### 1. Power Management

```
CONFIG_MTK_BASE_POWER=y                       # MTK power framework
CONFIG_MTK_CPU_FREQ=y                         # CPU frequency scaling
CONFIG_MTK_PTPOD=y                            # Power/thermal optimization
CONFIG_MTK_PTPOD_GPU=y                        # GPU power optimization
CONFIG_MTK_STATIC_POWER=y                     # Static power modeling
CONFIG_MTK_UNIFY_POWER=y                      # Unified power management
CONFIG_MTK_CM_MGR=y                           # Core manager
CONFIG_MTK_SWPM=y                             # Software power meter
CONFIG_MTK_QOS_FRAMEWORK=y                    # QoS framework
CONFIG_MTK_QOS_V2=y                           # QoS v2
CONFIG_MTK_LPM_MT6833=y                       # Low power modes
```

### 2. PMIC & Power Delivery

```
CONFIG_MTK_PMIC_NEW_ARCH=y                    # New PMIC architecture
CONFIG_MTK_PMIC_COMMON=y                      # PMIC common code
CONFIG_MTK_PMIC_CHIP_MT6359P=y                # MT6359P PMIC chip
CONFIG_MFD_MT6360_PMU=y                       # MT6360 PMU
CONFIG_MT6360_PMU_CHARGER=y                   # MT6360 charger
CONFIG_MT6360_PMIC=y                          # MT6360 PMIC
CONFIG_MT6360_LDO=y                           # MT6360 LDOs
CONFIG_MTK_EXTERNAL_CHARGER_TYPE_DETECT=y     # Charger detection
```

### 3. Display & Graphics

```
CONFIG_DRM_MEDIATEK=y                         # MediaTek DRM driver
CONFIG_MTK_FB=y                               # MediaTek framebuffer
CONFIG_MTK_DISP_PLATFORM="mt6853"             # Display platform
# CONFIG_DRM_MEDIATEK_HDMI is not set         # No HDMI support
```

### 4. Audio

```
CONFIG_SND_SOC_MEDIATEK=y                     # MediaTek audio SoC
CONFIG_SND_SOC_MT6833=y                       # MT6833 audio support
CONFIG_SND_SOC_MT6833_MT6359=y                # MT6833+MT6359 codec
CONFIG_MTK_AUDIO_TUNNELING_SUPPORT=y          # Audio offload
CONFIG_MTK_VOW_SUPPORT=y                      # Voice wakeup
```

### 5. Video Codec

```
CONFIG_VIDEO_MEDIATEK_JPEG=y                  # JPEG codec
CONFIG_VIDEO_MEDIATEK_VCU=y                   # Video codec unit
CONFIG_VIDEO_MEDIATEK_VCODEC=y                # Video encoder/decoder
# CONFIG_VIDEO_MEDIATEK_VCU_WO_FUSE is not set
```

### 6. Connectivity

#### WiFi
```
CONFIG_WLAN_VENDOR_MEDIATEK=y                 # MTK WiFi vendor
CONFIG_MTK_COMBO_WIFI=y                       # Combo WiFi chip
# Specific WiFi chip config in vendor modules
```

#### Bluetooth
```
CONFIG_MTK_COMBO=y                            # MTK combo chip (WiFi+BT)
# Bluetooth handled by combo chip driver
```

#### 5G Modem
```
# Modem support (proprietary modules)
CONFIG_MTK_ECCCI_DRIVER=y                     # CCCI driver (modem interface)
CONFIG_MTK_ECCCI_C2K=y                        # C2K modem support
```

### 7. Storage

```
CONFIG_MTK_UFS_SUPPORT=y                      # UFS storage
CONFIG_SCSI_UFSHCD=y                          # UFS host controller
CONFIG_SCSI_UFSHCD_PLATFORM=y                 # Platform UFS
CONFIG_MTK_UFS_LBA_CRC16_CHECK=y              # UFS data integrity
CONFIG_MTK_BLOCK_TAG=y                        # Block I/O tagging
```

### 8. Security

```
CONFIG_DEVAPC_MT6833=y                        # Device access permission
CONFIG_DEVMPU_MT6833=y                        # Device memory protection
CONFIG_MTK_SEC_VIDEO_PATH_SUPPORT=y           # Secure video
CONFIG_MTK_TEE_GP_SUPPORT=y                   # TEE support
CONFIG_ARM64_SW_TTBR0_PAN=y                   # PAN emulation
CONFIG_RANDOMIZE_BASE=y                       # KASLR
```

### 9. Sensors

```
CONFIG_MTK_SENSORS_1_0=y                      # Sensor framework 1.0
# Actual sensor drivers in vendor modules
```

### 10. Camera

```
CONFIG_MTK_CAMERA_ISP_SUPPORT=y               # ISP support
# Camera HAL and drivers in vendor
```

## Memory Configuration

```
CONFIG_SWAP=y                                 # Swap support
# CONFIG_SYSVIPC is not set                   # No SysV IPC
# CONFIG_POSIX_MQUEUE is not set              # No POSIX mqueues
CONFIG_CROSS_MEMORY_ATTACH=y                  # Process memory attach
CONFIG_CMDLINE="console=tty0 console=ttyMT3,921600n1 root=/dev/ram vmalloc=496M slub_max_order=0 slub_debug=O"
```

## File Systems

```
CONFIG_EXT4_FS=y                              # ext4
CONFIG_EXT4_FS_SECURITY=y                     # ext4 security
CONFIG_F2FS_FS=y                              # F2FS
CONFIG_F2FS_FS_SECURITY=y                     # F2FS security
CONFIG_SDCARD_FS=y                            # SDcard FS
CONFIG_PSTORE=y                               # Persistent storage
CONFIG_PSTORE_CONSOLE=y                       # Pstore console
CONFIG_PSTORE_RAM=y                           # Pstore RAM backend
```

## Android-Specific

```
CONFIG_ANDROID=y                              # Android support
CONFIG_ANDROID_BINDER_IPC=y                   # Binder IPC
CONFIG_ANDROID_BINDERFS=y                     # Binder FS
CONFIG_ASHMEM=y                               # Android shared memory
CONFIG_ANDROID_LOW_MEMORY_KILLER=y            # LMK
CONFIG_ANDROID_VSOC=y                         # Virtual SoC
```

## Network & Connectivity

```
CONFIG_INET=y                                 # IPv4
CONFIG_IPV6=y                                 # IPv6
CONFIG_NETFILTER=y                            # Netfilter
CONFIG_NF_CONNTRACK=y                         # Connection tracking
CONFIG_NETFILTER_XT_TARGET_TCPMSS=y           # TCP MSS
CONFIG_IP_NF_IPTABLES=y                       # iptables
CONFIG_IP6_NF_IPTABLES=y                      # ip6tables
```

## Debugging & Tracing

```
CONFIG_AUDIT=y                                # Audit framework
CONFIG_AUDITSYSCALL=y                         # Syscall auditing
CONFIG_FTRACE=y                               # Function tracing
CONFIG_FUNCTION_TRACER=y                      # Function tracer
CONFIG_DYNAMIC_FTRACE=y                       # Dynamic ftrace
# CONFIG_KASAN is not set                     # No KASAN (not enabled)
# CONFIG_KMEMLEAK is not set                  # No memleak detection
```

## Boot Configuration

```
CONFIG_CMDLINE_FROM_BOOTLOADER=y              # Use bootloader cmdline
CONFIG_BUILD_ARM64_APPENDED_DTB_IMAGE=y       # Append DTB to kernel
```

## Notable Disabled Features

```
# CONFIG_ARCH_MEDIATEK is not set             # Generic MTK arch disabled (using specific)
# CONFIG_KASAN is not set                     # Kernel address sanitizer
# CONFIG_UBSAN is not set                     # Undefined behavior sanitizer  
# CONFIG_KMEMLEAK is not set                  # Kernel memory leak detector
# CONFIG_DEBUG_KMEMLEAK is not set            # Debug memleak
# CONFIG_SLUB_DEBUG_ON is not set             # SLUB debugging off
```

## Build Optimizations

```
CONFIG_CC_OPTIMIZE_FOR_PERFORMANCE=y          # Optimize for performance
# CONFIG_CC_OPTIMIZE_FOR_SIZE is not set      # Not optimizing for size
```

## Summary

This configuration represents a **production-ready, performance-optimized** kernel for the MT6833 platform with:

- ✅ All MediaTek platform drivers enabled
- ✅ Power management fully configured
- ✅ Security features enabled (DEVAPC, DEVMPU)
- ✅ All hardware peripherals supported
- ✅ Android-specific features enabled
- ✅ Optimized for performance
- ❌ Debug features disabled (production build)
- ❌ KASAN/UBSAN disabled (performance)

This is the **exact configuration** used in the stock firmware and can be used as-is for LineageOS builds or as a base for custom configurations.
