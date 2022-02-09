# ASUS B460 Strix ITX OpenCore EFI

The Hackintosh is based on OpenCore `0.7.7` at the time of writing, and `macOS Monterey 12.2` following the Dortania [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/) for [Comet Lake](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#starting-point).

Hackintosh EFI for `ASUS ROG STRIX B460I` + `Intel Core i7 10700` + `BCM94360CS2 Wireless Air Port Card`

![](https://raw.githubusercontent.com/yqlbu/asus-b460i-strix-oc-efi/master/assets/screenshot.png)

## Hardware

* Case: NZXT H1 Case ( come with AIO cooler, 650W power supply and PCIE Riser Card )
* Motherboard: Asus ROG STRIX B460-I
* WiFi module: BCM94360CS2 Wireless Air Port Card (Driverless)
* CPU: Intel Core i7-10700
* GPU: Intel UHD630 and Sapphire Pulse RX 5500 XT
* RAM: CORSAIR VENGEANCE LPX DDR4 3000 32GB(16G×2)
* Storage: Western Digital SN750 512GB M.2-2280 NVME

## Details

### BIOS

There is no CFG-lock issue with this board. Installing BIOS version 0707 is worth it as it enables higher resolutions in the boot loader screen for me.

Things I changed from default:

* Fast boot: OFF
* Intel Virtualization Technology: ON
* OS type: Windows UEFI
* Multi Monitor support: ON
* Clear the platform key as this disables secure boot.

### SSDTs

Compiled by following the [Dortania's ACPI Guide](https://dortania.github.io/Getting-Started-With-ACPI/)

* SSDT-AWAC (enable the legacy RTC clock)
* SSDT-EC-USBX (Fix embedded controller)
* SSDT-PLUG (Power management)
* SSDT-RHUB (reset USB controller)
* SSDT-SBUS-MCHC (SMBus support)
* [SSDT-RX5700XT](https://www.tonymacx86.com/threads/amd-radeon-performance-enhanced-ssdt.296555/) (Better support for RX5600/5700)

### Kexts

Download them from their official repo

* [AppleALC.kext](https://github.com/acidanthera/AppleALC) - Audio
* [FakePCIID.kext](https://github.com/RehabMan/OS-X-Fake-PCI-ID) and FakePCIID_Intel_HDMI_Audio.kext - Also needed for audio to work
* [IntelMausi.kext](https://github.com/acidanthera/IntelMausi) - Ethernet
* [Lilu.kext](https://github.com/acidanthera/Lilu) - Enables various patching
* [NVMeFix.kext](https://github.com/acidanthera/NVMeFix) - Better NVMe support
* [VirtualSMC](https://github.com/acidanthera/VirtualSMC) SMCProcessor.kext, SMCSuperIO.kext, VirtualSMC.kext - SMC emulator
* USB-Map.kext - Available from the kexts folder in this repo. This maps the 6 USB3 ports and the two internal ones used for Bluetooth and the Aura header. See USB section.
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen) - Various graphics related patches
* [XHCI-unsupported.kext](https://github.com/RehabMan/OS-X-USB-Inject-All) - There is a patched version of this in this repo. Needed for USB3 to work.
* [DAGPM.kext](https://www.tonymacx86.com/threads/amd-radeon-performance-enhanced-ssdt.296555/) - Better power management for AMD Navi GPUs.
* [HibernationFixup.kext](https://github.com/acidanthera/HibernationFixup) - Added this back as it seems like my computer crashed when in sleep mode for more than 24h. Need more testing to see if this fixes it though.

### USB

This board has two USB controllers. The Intel one that drives the 6 USB3 ports on the rear panel as well as Bluetooth and the Aura header. I'm not using the internal USB ports - so the supplied USB Map will not map these. Currently 14 ports are mapped - so there is room for one more logical port. The second controller is for the rear USB-C port and it doesn't need a USB map.

The front USB ports that I didn't map have the following IDs (thanks to [zhzhzh88](https://www.reddit.com/r/hackintosh/comments/hbcdgq/asus_rog_strix_b460i_gaming_mobo_hackintosh/g8cmw5b?utm_source=share&utm_medium=web2x&context=3)):

* HS01, port 0x01 (USB2)
* HS02, port 0x02 (USB2)
* SS01, port 0x11 (USB3)
* SS02, port 0x12 (USB3)

In addition to the USB-Map.kext you also need the modified `XHCI-unsuported.kext` to enable USB3 ports.

### Note on Navi GPU

I found that installing the kext and SSDT from [here](https://www.tonymacx86.com/threads/amd-radeon-performance-enhanced-ssdt.296555/) not only improves Geekbench scores (see below), but also real world performance in Mafia III. Without it the GPU seemed to thermal throttle after a few minutes of playing and the frame rate would drop really low. Interestingly I did not see this happen with [Unigine Heaven](https://benchmark.unigine.com/heaven) which is much harder on the GPU.

### Config.plist

#### Kernel

 Quirks > DisableRtcChecksum = TRUE - This prevents the BIOS from restarting into safe mode
 Misc > Boot > HibernateMode = Auto - Not sure if this is necessary. The machine sleeps fine without this, but maybe this enables deeper hibernation.
 All other settings follow the Dortania guide.

#### PlatformInfo

I used the iMac19,1 SMBIOS because that was what the guide recommended at the time. It has now been updated to use iMac20,1 instead. So I would use this for a new build. But since I haven't found any issues with iMac19,1 I see no reason to change it. 

## Benchmarks

| Items                                                        | Scores                           |
| :----------------------------------------------------------- | :------------------------------- |
| CPU - Geekbench                                              | Single / Multi-Core: 1262 / 7773 |
| Intel UHD630 - Geekbench                                     | OpenCL / Metal: 5319 / 4972      |
| RX 5500 XT - Geekbench ([with Radeon performance improvements](https://www.tonymacx86.com/threads/amd-radeon-performance-enhanced-ssdt.296555/)) | OpenCL / Metal: 37937/ 39645     |

## OC Version tags

- [0.7.7](https://github.com/yqlbu/Hackintosh-EFI/releases/tag/v0.7.7)
- [0.7.6](https://github.com/yqlbu/Hackintosh-EFI/releases/tag/v0.7.6)
- [0.7.3](https://github.com/yqlbu/Hackintosh-EFI/releases/tag/v0.7.3)
- [0.7.1](https://github.com/yqlbu/Hackintosh-EFI/releases/tag/v0.7.1)
- [0.6.8](https://github.com/yqlbu/Hackintosh-EFI/releases/tag/v0.6.8)

## Source Code

- [OpenCore bootloader](https://github.com/acidanthera/OpenCorePkg)
- [OpenCore BinaryData](https://github.com/acidanthera/OcBinaryData)

## Useful Tools for Hackintosh

- [OpenCore QtOpenCoreConfig](https://github.com/ic005k/QtOpenCoreConfig)
- [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/)
- [OC Builder](https://github.com/Pavo-IM/ocbuilder)
- [Hackintools](https://github.com/headkaze/Hackintool)
- [OC-Gen-X](https://github.com/Pavo-IM/OC-Gen-X)
- [Propertree](https://github.com/corpnewt/ProperTree)
- [OpenCore Official Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [OpenCore Sanity Checker](https://opencore.slowgeek.com/)

