# 锐龙黑苹果 - 华硕电竞特工B550M(WIFI版)Opencore引导文件

[**English**](README_en.md)| [**中文**](README.md)

## 硬件配置
| **组件** | **型号** |
| ------------- | --------- |
| CPU | AMD 锐龙5 5600X @ 3.6GHz OC|
| 主版 | 华硕 电竞特工 TUF Gaming B550M-Plus (WI-FI) |
| 内存 | 英睿达 DDR4 16GB (2 x 8GB) @3600(OC3800)|
| 声卡 | 瑞昱 ALCS-1200A |
| 显卡 | 迪兰恒进 RX 5500XT 8G |
| 网卡 | 瑞昱 RTL8125 2.5GbE |
| WiFi蓝牙 | 英特尔 WiFi 6 AX200 |
| 电源 | 追风者 Revolt PRO 850W |
| 系统硬盘 | 惠普 S700 128G |

**macOS 版本**: 12.1  (21C52) 

**OpenCore 版本**: 0.7.6

**机型**:  iMacPro1,1

## 目录
 - [更新日志](#更新日志)
 - [驱动和扩展](#驱动和扩展)
 - [如何使用](#如何使用)
 - [BIOS设置](#BIOS设置)
 - [适用](#适用)
 - [睡眠信息](#睡眠信息)
 - [PAT补丁信息](#PAT补丁信息)
 - [Adobe系列软件修复](#Adobe系列软件修复)
 - [虚拟化](#虚拟化)
 - [安装向导](#安装向导)

 
## 更新日志
  1. 系统版本升级到12.1
  2. 更换并适配了opencore主题
  3. 修复蓝牙问题导致启动在ALUC卡住启动慢的问题。
  4. 修复HP SSD未开启Trim 系统卡顿的问题。
 

## 驱动和扩展
 - [[引导] OpenCore](https://github.com/acidanthera/OpenCorePkg)
 - [[资源] Picker GUI](https://github.com/acidanthera/OcBinaryData/tree/master/Resources)
 - [[补丁] AMD_Vanilla](https://github.com/AMD-OSX/AMD_Vanilla)
 - [[驱动] FwRuntimeServices](https://github.com/acidanthera/OpenCorePkg)
 - [[驱动] HfsPlus](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
 - [[驱动] OpenHfsPlus](https://github.com/acidanthera/OpenCorePkg)
 - [[驱动] OpenRuntime](https://github.com/acidanthera/OpenCorePkg)
 - [[驱动] OpenCanopy](https://github.com/acidanthera/OpenCorePkg)
 - [[扩展] Lilu](https://github.com/acidanthera/Lilu)
 - [[扩展] VirtualSMC](https://github.com/acidanthera/VirtualSMC)
 - [[扩展] WhateverGreen](https://github.com/acidanthera/WhateverGreen)
 - [[扩展] AppleALC 声卡驱动](https://github.com/acidanthera/AppleALC)
 - [[扩展] AppleMCEReporterDisabler 关闭AppleMCERReport](https://github.com/AMD-OSX/AMD_Vanilla/raw/master/Extra/AppleMCEReporterDisabler.kext.zip)
 - [[扩展] LucyRTL8125Ethernet 2.5G有线网卡驱动](https://github.com/Mieze/LucyRTL8125Ethernet)
 - [[扩展] itlwm Intel AX200 无线网卡驱动](https://github.com/OpenIntelWireless/itlwm)
 - [[扩展] IntelBluetoothFirmware Intel 蓝牙驱动](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
 - [[扩展] AMDRyzenCPUPowerManagement](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[扩展] SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[扩展] NVMeFix](https://github.com/acidanthera/NVMeFix)
 - [[扩展] RestrictEvents](https://github.com/acidanthera/RestrictEvents)
 - [[扩展] Innie](https://github.com/cdf/Innie/releases)
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

  如果无法正常启动,检查:
  1. kernel > Quirks中ProvideCurrentCpuInfo是否设置为True.(必须启用,否则无法启动).
  2. Misc -> Security -> SecureBootModel是否为Disabled
  3. kernel > Patch 中 algrey - Force cpuid_cores_per_package 是否已经按CPU核心数进行更改,具体方法见[AMD_Vanilla
](https://github.com/AMD-OSX/AMD_Vanilla).
  
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
| TPM Device | 关闭 <sup>2</sup>|


<sup>1</sup> 这里如果开启的话,**必须**在config.plist配置文件的`boot-args`项中删除  `npci=0x2000`,不过推荐主板关闭,使用参数

<sup>2</sup> TPM安装阶段关闭,安装完成后可以开启,特别是win11双系统的话,不开启无法启动win11

**这些选项大多可能不存在于您的主板bios选项中，只需尽可能接近即可。如果您的BIOS中没有其中许多选项，请不要太担心**

**在启动macOS之前，请记住将BIOS更新到最新版本**

## 适用
适用于大多数具有17h和19h的AMD CPU, 所有Ryzen系列和Athlon 2xxGE。
不适用于15h（FX系列）、16h（A系列）和Threadripper CPU。

详情见[**支持列表**](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/CPU.html) 

**集成显卡不能正常工作**，NVIDIA显卡具体看[**这里**](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/nvidia-gpu.html)

如果你是N卡用户，你可能需要选择Algrey版本的PAT补丁，具体看[**这里**](#PAT补丁信息)

**B550和A520主板**需要添加**SSDT-CPUR**这个ACPI补丁才能正常启动。[**下载地址**](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml) \
下载后放到`OC/ACPI` 目录下，并在配置文件config.plist中启用。

**B550, A520主板以及使用最新bios版本的B450, X470, X570主板** 必须将config中`SetupVirtualMap` 禁用。具体路劲为 `Booter -> Quirks -> SetupVirtualMap` ，将值改为 `false`

**AMD Navi 显卡 (比如RX 5500, 5600, 5700)** 应在启动参数`boot-args` 中添加 `agdpmod=pikera` 以修复黑屏错误。

如果你的声卡有问题，你必须改变`alcid`的值来适配你的主板，具体见[**这里**](https://github.com/acidanthera/applealc/wiki/supported-codecs) 。你可以尝试不同的layout-id值，直到你声卡正常工作。

如果你有网络连接问题，可能是网卡驱动不适合，请按手册查找自己主板的网卡驱动，[**详见这里**](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#ethernet) 

PAT补丁默认启用的是Shaneee版本，可以提供显卡的性能，但同时也会带来一些兼容性的问题，如果兼容性有问题，请切换到另一个PAT补丁，具体信息见[**PAT补丁信息**](#PAT补丁信息)

## 睡眠信息

如果你有睡眠问题，首先请定制你的USB端口，定制方法 [**参考这里**](https://dortania.github.io/OpenCore-Post-Install/usb/)，如果定制USB仍然存在问题，你应该尝试通过SSDT来修复USB。

在SSDT-SLEEP.aml中有用于修补_STA方法的补丁。补丁适用于_SB.PCI0.GPP2.PTXH和_SB.PCI0.GP17.XHC0USB控制器，如果你的USB控制器还有其他地址，你必须在SSDT添加。补丁程序仅适用于macOS，因此其他系统上的USB不受此补丁的影响。

睡眠问题总是由于USB引起的，但也不是肯定就是USB的问题，如果USB补丁无效的话，参考[**这篇文章**](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html) 来修复睡眠。

## PAT补丁信息
| **Shaneee's** | **Algrey's** |
| ------------- | --------- |
| 更好的GPU性能 | 更差的GPU性能 |
| 可能不适用于NVIDIA GPU | 与所有GPU兼容 |
| HDMI / DP音频可能不起作用 | HDMI/DP 音频正常工作 |
| 默认启用 | 	默认禁用 |


要切换到另一个补丁，请在config.plist中搜索mtrr_update_action。然后要使用的补丁Enable设置成TRUE，另一个设置成FALSE。

不要尝试同时两个补丁，必须禁用一个。


## Adobe系列软件修复

由于缺少intel_fast_memset指令，Adobe应用程序在AMD黑苹果上会崩溃。你可以运行[**这个脚本**](/Resources/Adobe%20patch.sh)来解决，或者按照[**这篇教程**](https://gist.github.com/mikigal/8e1f804fcd7dbafbded2f236653be7c8)来手动修复！切记修补后重启系统。

如果从文件中打开图像时Photoshop崩溃，则必须将其降级到22.0版

## 虚拟化

首先，您必须在BIOS设置中启用`SVM`。
Parallels Desktop（仅适用于13.1，更高版本需要AppleHV）和VirtualBox（其工作原理比Parallels差得多）这两款虚拟化软件支持。
VMWare Fusion 10在Big Sur上不能使用，在Catalina上，它需要这种[**解决方法**](https://posts.boy.sh/vmware-fusion-catalina) \
Docker也无法正常工作。您必须使用Docker Toolbox，但是它不具备Docker的所有功能。



在Big Sur (11.0)上 Parallel无法正常启动，会提示 `Required components are missing from the OS` 错误。你必须在安装时添加`SYSTEM_VERSION_COMPAT=1` 参数。 \
在终端中运行如下命令: `SYSTEM_VERSION_COMPAT=1 open /Volumes/Parallels\ Desktop\ 13.1.0/Install.app/`, 将路径替换成Parallel安装文件所在路径 \

安装完成后启动Parallels时也会出现同样的错误，你可以每次启动时添加同样的参数，也可以使用大神制作的启动器，[**下载地址**](/Resources/Parallels%20Desktop%20Launcher.app.zip)

Parallels 13.1仅支持Windows10 1607版本以及更老的版本。较新的版本在安装时会卡住。建议使用Windows 7，效果会更好。不要使用自动安装功能。

不要向虚拟机添加太多资源，会导致性能问题。
我测试了许多VM配置-最佳性能结果如下：

Parallels Desktop 13.1
4个CPU核心
4GB内存
1GB VRAM
3D加速：DirectX 9
操作系统：禁用Aero主题的Windows 7（SP1，内部版本7601）

如果虚拟机操作系统看不到USB设备将其重新连接到另一个端口，则通常可以解决此问题。
如果[**Coherence 模式**](https://www.parallels.com/blogs/how-to-use-coherence-mode-in-parallels-desktop/)不起作用，则必须禁用虚拟机的防病毒软件或将以下文件添加到其排除列表中：

  - `C:\Program Files (x86)\Parallels\Parallels Tools\Services\coherence.exe`
  - `C:\Program Files (x86)\Parallels\Parallels Tools\Services\prl_hook.dll`

## 安装向导
**如果您在安装或启动 macOS 时遇到任何问题、内核崩溃或其他系统相关问题，请查看 OC 配置指南**

**如果其他东西不能正常工作（例如USB端口、iServices、DRM/Netflix），请查看安装后指南**

 - 创建USB安装程序: [**\*点击\***](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
 - OpenCore配置: [**\*点击\***](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html)
 - 安装后: [**\*点击\***](https://dortania.github.io/OpenCore-Post-Install/)
 - 故障诊断: [**\*点击\***](https://dortania.github.io/OpenCore-Post-Install/)
 - ACPI补丁: [**\*点击\***](https://dortania.github.io/Getting-Started-With-ACPI/)
 - USB映射: [**\*点击\***](https://dortania.github.io/OpenCore-Post-Install/usb/)





 
