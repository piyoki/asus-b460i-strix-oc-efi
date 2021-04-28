# Hackintosh EFI

Hackintosh EFI for `ASUS B460` + `Intel Core i7 10700`

## OC Version tags

- [0.6.8](https://github.com/yqlbu/Hackintosh-EFI/releases/tag/v0.6.8)

## Upgrade Guide

**Step 0** -- Download the latest version of OC from [https://github.com/acidanthera/OpenCorePkg/releases](https://github.com/acidanthera/OpenCorePkg/releases), find the file named “OpenCanopy.efi” from `x64` >> `EFI` >> `OC` >> `Drivers`, drag it out for later use

**Step 1** -- Download the latest GUI driver from [https://github.com/acidanthera/OcBinaryData](https://github.com/acidanthera/OcBinaryData) and copy the `Resource` folder over to the new `EFI`

**Step 2** -- Use [OC Gen-X](https://github.com/Pavo-IM/OC-Gen-X)) to generate the latest version of `OC`

**Step 3** -- Copy the `ACPI` and `KEXT` files from the older version of OC to the newer version of OC

**Step 4** -- Copy the previous version of `config.plist` to the new `EFI` folder

**Step 5** -- Open the `config.plist` with [Propertree](https://github.com/corpnewt/ProperTree) then use `Cmd + R` to load the new drivers to the `config.plist`

**Step 6** -- Modified `Misc` > `PickerMode` set from `Builtin` to `External`, `ShowPicker` to `True` in `config.plist`


## Source Code

- [OpenCore bootloader](https://github.com/acidanthera/OpenCorePkg)
- [OpenCore BinaryData](https://github.com/acidanthera/OcBinaryData)

## Useful Tools for Hackintosh

- [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/)
- [OC Builder](https://github.com/Pavo-IM/ocbuilder)
- [Hackintools](https://github.com/headkaze/Hackintool)
- [OC-Gen-X](https://github.com/Pavo-IM/OC-Gen-X)
- [Propertree](https://github.com/corpnewt/ProperTree)
- [OpenCore Official Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [OpenCore Sanity Checker](https://opencore.slowgeek.com/)
