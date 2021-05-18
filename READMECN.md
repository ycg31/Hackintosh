# AMD Ryzen Hackintosh - Opencore EFI for Asus TUF Gaming B550M-Plus (WI-FI)


## Specification
| **Component** | **Model** |
| ------------- | --------- |
| CPU | AMD Ryzen 5 5600X @ 3.6GHz OC|
| 主版 | Asus TUF Gaming B550M-Plus (WI-FI) |
| 内存 | Crucial 英睿达 DDR4 16GB (2 x 8GB) @3600(OC3800)|
| 声卡 | ALCS-1200A |
| 显卡 | DATALAND 迪兰恒进 RX 5500XT 8G |
| 网卡 | RTL8125 2.5GbE |
| WiFi蓝牙 | Intel WiFi 6 AX200 |
| 电源 | PHANTEKS 追风者 Revolt PRO 850W |
| 系统硬盘 | HP S700 128G |

**macOS 版本**: 11.3.1  (20E241) 

**OpenCore 版本**: 0.7.0

**机型**:  iMacPro1,1

## 目录
 - [驱动和扩展](#驱动和扩展)
 - [如何使用](#如何使用)
 - [BIOS设置](#BIOS设置)
 - [软件适用性](#软件适用性)
 - [睡眠信息](#睡眠信息)
 - [PAT补丁信息](#PAT补丁信息)
 - [Adobe系列软件修复](#Adobe系列软件修复)
 - [虚拟化](#虚拟化)
 - [安装向导](#安装向导)

 
## 驱动和扩展
 - [[Bootloader] OpenCore](https://github.com/acidanthera/OpenCorePkg)
 - [[Resources] Picker GUI](https://github.com/acidanthera/OcBinaryData/tree/master/Resources)
 - [[Patch] AMD_Vanilla](https://github.com/AMD-OSX/AMD_Vanilla)
 - [[Driver] FwRuntimeServices](https://github.com/acidanthera/OpenCorePkg)
 - [[Driver] HfsPlus](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
 - [[Driver] OpenHfsPlus](https://github.com/acidanthera/OpenCorePkg)
 - [[Driver] OpenRuntime](https://github.com/acidanthera/OpenCorePkg)
 - [[Driver] OpenCanopy](https://github.com/acidanthera/OpenCorePkg)
 - [[Kext] Lilu](https://github.com/acidanthera/Lilu)
 - [[Kext] VirtualSMC](https://github.com/acidanthera/VirtualSMC)
 - [[Kext] WhateverGreen](https://github.com/acidanthera/WhateverGreen)
 - [[Kext] AppleALC 声卡驱动](https://github.com/acidanthera/AppleALC)
 - [[Kext] AppleMCEReporterDisabler 关闭AppleMCERReport](https://github.com/AMD-OSX/AMD_Vanilla/blob/opencore/Extra/AppleMCEReporterDisabler.kext.zip)
 - [[Kext] LucyRTL8125Ethernet 2.5G有线网卡驱动](https://github.com/Mieze/LucyRTL8125Ethernet)
 - [[Kext] itlwm Intel AX200 无线网卡驱动](https://github.com/OpenIntelWireless/itlwm)
 - [[Kext] IntelBluetoothFirmware Intel 蓝牙驱动](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
 - [[Kext] AMDRyzenCPUPowerManagement](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[Kext] SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[Kext] NVMeFix](https://github.com/acidanthera/NVMeFix)
 - [[Kext] RestrictEvents](https://github.com/acidanthera/RestrictEvents)
 - [[SSDT] EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
 - [[SSDT] SLEEP-PTXH](./OC/ACPI/SSDT-SLEEP-PTXH.aml)



## 如何使用
  1. 使用[**本指南**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)制作USB安装程序
  2. 克隆存储库，并将“BOOT”和“OC”目录粘贴到您的引导驱动器“EFI”文件夹中
  3. 下载 [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS)以生成唯一的SMBIOS信息。运行它并选择生成SMBIOS，因为型号选择iMacPro1,1。
  4. 使用[**ProperTree**](https://github.com/corpnewt/ProperTree)打开config.plist，然后转到PlatformInfo > Generic。将MLB（板串行）、SystemSerialNumber（串行）和SystemUUID（SmUUID）设置为生成的值。将ROM更改为去掉:的网卡MAC地址。[**如何获取MAC地址？**](https://www.wikihow.com/Find-the-MAC-Address-of-Your-Computer)
  5. 将您的BIOS更新到最新版本，并将其设置设置为[**所需的值**](#BIOS设置)
  6. 阅读有关某些硬件所需更改的[**信息**](#软件适用性)
  7. 启动并安装它！
  8. 安装后，您可以将 EFI 目录复制到磁盘的 EFI 分区 - 然后您可以无需U盘即可启动 macOS
  9. 如果使用双系统必须开启Bootstrap,他将保护你的Opencore不被Windows的引导覆盖, 点击获取相关信息[**信息**](https://dortania.github.io/OpenCore-Post-Install/multiboot/bootstrap.html)。
  
**你不能直接使用本库中的SMBIOS信息,必须自己生成并保持唯一。**

## BIOS设置

| **Option** | **Status** |
| ------------- | --------- |
| SATA 模式 | AHCI |
| Above 4G Decoding | 开启 <sup>1</sup> |
| EHCI/XHCI Hand-off | 开启 |
| SVM | 开启 |
| CSM | 关闭 |
| Resizable BAR Support | 关闭 |
| 安全启动 | 关闭 |
| 串口 | 关闭 |
| Parallel Port | 关闭 |


<sup>1</sup> 这里如果开启的话,**必须**在config.plist配置文件的`boot-args`项中删除  `npci=0x2000`,不过推荐主板关闭,使用参数

**这些选项大多可能不存在于您的主板bios选项中，只需尽可能接近即可。如果您的BIOS中没有其中许多选项，请不要太担心**

**在启动macOS之前，请记住将BIOS更新到最新版本**

## 软件适用性
大多数具有17H和19H（所有Ryzen的世代，Athlon 2xxGE）的CPU与macOS兼容外设的CPU应该可以使用此存储库的EFI工作。
这里不涵盖对15小时（FX系列）、16小时（A系列）和Threadripper CPU的支持。

Most builds with **17h and 19h (All Ryzen's generations, Athlon 2xxGE)** CPUs with [**macOS compatible peripherals**](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/CPU.html) should work with EFI from this repository. \
**Support for 15h (FX series), 16h (A series) and Threadripper CPUs is not covered here.**

Integrated GPUs **DO NOT WORK**, for NVIDIA check details [**here**](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/nvidia-gpu.html) (it's not covered in this repository). \
If you have **NVIDIA GPU** you may have to change PAT Patch to Algrey's version, read [**here**](#PAT-patch-information) about it

Motherboards with **B550 and A520** chipsets require additional **SSDT-CPUR** to boot macOS. \
You have to [**download it**](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml) and put it under `OC/ACPI` directory. Then you have to add it to your config. Open it with ProperTree or your favourite text editor and add it under `ACPI -> Add`. You should do this in the same way as you did `SSDT-EC-USBX-DESKTOP`, just change the name of the file.

For **B550, A520 and B450, X470, X570 with newer BIOS versions** `SetupVirtualMap` must be disabled. Go to `Booter -> Quirks -> SetupVirtualMap` in your config and change it to `false`

For **AMD Navi GPUs (RX 5500, 5600, 5700)** you have to add `agdpmod=pikera` to `boot-args` to fix black screen issue.

If you experience issues with your audio, then you have to change `alcid` proper for your audio chipset. Find your chipset [**here**](https://github.com/acidanthera/applealc/wiki/supported-codecs) and try setting `alcid` in `boot-args` parameter to every layout-id values from AppleALC wiki until you get correct value (working audio inputs and outputs) for your motherboard.

If you experience issues with network connection, then you probably have another ethernet chipset. Click [**here**](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#ethernet) for information about kexts for ethernet cards. \
For High Sierra use [**this kext**](https://bitbucket.org/RehabMan/os-x-realtek-network/downloads/) for Realtek 8111 ethernet card, because version from this repository needs Mojave or newer version. \
If you are using Big Sur with RTL8111 but network is unstable try [**this version**](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases/tag/v2.2.2) of kext. \
Remember to remove `RealtekRTL8111.kext` before use another kext.

By default enabled is PAT patch made by Shaneee - it improves GPU performance but can cause some issues. It can break HDMI audio and make builds with NVIDIA GPU unbootable. You can switch patch with better compatibility (but worse performance). Click [**here**](#PAT-patch-information) for more information.

## 睡眠信息
If you have issues with sleep, firstly you have to map your USB ports. You can read about it [**here**](https://dortania.github.io/OpenCore-Post-Install/usb/). If map does not help, you should try patching USB via SSDT.

In `SSDT-SLEEP.aml` there are patches for _STA method. Patch as applied to `_SB.PCI0.GPP2.PTXH` and `_SB.PCI0.GP17.XHC0` USB controllers, if you have other addresses of USB controllers you have to edit SSDT for your build. Patch is applied only for macOS, so USB on other systems should work normally.

Sleep in AMD systems is often broken by USB issues, but not always. If USB patching does not help read [**this guide**](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html) about fixing sleep.

## PAT补丁信息
| **Shaneee's** | **Algrey's** |
| ------------- | --------- |
| Much better GPU performance | Worse GPU performance |
| May not work with NVIDIA GPUs | Compatible with all GPUs |
| HDMI/DP audio may not work | HDMI/DP audio works |
| Enabled by default | Disabled by default |

To switch to another patch search for `mtrr_update_action` in `config.plist`. Then set `Enabled` to `true` for patch which you want to use. Remember to set `Enabled` to `false` for second PAT patch.

**Don't try to use them both at the same time, it won't work.**

## Adobe系列软件修复
Adobe applications crash on AMD Hackintoshes due to missing intel_fast_memset instructions.
Run [**this script**](/Resources/Adobe%20patch.sh) or if you prefer to do it manually follow [**this guide**](https://gist.github.com/mikigal/8e1f804fcd7dbafbded2f236653be7c8) to get it working! Remember to reboot your Hackintosh after patching.

If Photoshop crashes while opening image from file you have to downgrade it to version 22.0

## 虚拟化
Firstly you have to enable `SVM` in your BIOS settings. \
Parallels Desktop (only up to 13.1, newer version require AppleHV) and VirtualBox (it works much worse than Parallels) are only compatible software for virtual machines. There's also VMWare Fusion 10, but it's totally broken on Big Sur, on Catalina it needs [**this workaround**](https://posts.boy.sh/vmware-fusion-catalina) \
Docker also does not work - you have to use Docker Toolbox instead, but it does not have all Docker's features.

On Big Sur (11.0) Parallel's won't start - it will show `Required components are missing from the OS` error due to changed versions number schema. You have to run installer from with `SYSTEM_VERSION_COMPAT=1` parameter. \
Open your Terminal app and run Parallel's installer like this: `SYSTEM_VERSION_COMPAT=1 open /Volumes/Parallels\ Desktop\ 13.1.0/Install.app/`, just replace volume's name to proper for your Parallel's DMG. \
Same problem will exist while trying to start installed Parallels - you can run it every time with the same way as installer or use my launcher (it simply starts Parallels with required parameter) - you can get it [**here**](/Resources/Parallels%20Desktop%20Launcher.app.zip)

Parallels 13.1 support only Windows 10 Anniversary Update (build 1607) and older versions. Newer versions stuck while installing. Also I recommend using Windows 7 - it works much better. Do not use automatical installation feature - it caused some issue for me.

**DO NOT** add too much resources to virtual machines, it causes performance issues independently of host specification. \
I tested lot of VM configurations - the best performance results gives:
  - Parallels Desktop 13.1
  - 4 CPU cores
  - 4GB RAM
  - 1GB VRAM
  - 3D Acceleration: DirectX 9
  - OS: Windows 7 (SP1, build 7601) with disabled Aero theme

With above configuration system is generally responsive, it runs simple games (e. g. The Binding of Isaac: Repentace) smoothly too. All Parallels host-integration features works great.

If guest OS does not see USB device reconnecting it to another port usually solve this issue. \
If [**Coherence Mode**](https://www.parallels.com/blogs/how-to-use-coherence-mode-in-parallels-desktop/) does not work you have to disable guest's antivirus or add these files to it's exclusions list:
  - `C:\Program Files (x86)\Parallels\Parallels Tools\Services\coherence.exe`
  - `C:\Program Files (x86)\Parallels\Parallels Tools\Services\prl_hook.dll`

## 安装向导
**如果您在安装或启动 macOS 时遇到任何问题、内核崩溃或其他系统相关问题，请查看 OC 配置指南**

**如果其他东西不能正常工作（例如USB端口、iServices、DRM/Netflix），请查看安装后指南**

 - 创建USB安装程序: [**\*点击\***](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
 - penCore配置: [**\*点击\***](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html)
 - 安装后: [**\*点击\***](https://dortania.github.io/OpenCore-Post-Install/)
 - 故障诊断: [**\*点击\***](https://dortania.github.io/OpenCore-Post-Install/)
 - ACPI补丁: [**\*点击\***](https://dortania.github.io/Getting-Started-With-ACPI/)
 - USB映射: [**\*点击\***](https://dortania.github.io/OpenCore-Post-Install/usb/)





 