# 微星B460M MORTAR WIFI i7-10700 核显 黑苹果 OpenCore驱动

## 系统信息

OpenCore版本：0.6.9

MacOS版本：big sur 11.3.1

可用功能：以太网、wifi、蓝牙、USB映射、节能五项。。。

遗留问题：

1. 关机后自动重启，解决办法：在BIOS禁用USB唤醒，路径：Settings/Advanced/Wake Up Event Setup/Resume By USB Device，这样会产生另一个问题，鼠标和键盘无法唤醒，但是可以使用电源键唤醒。希望有更优方案的大神分享一下
2. 双屏幕开机会花屏，解决办法：单屏幕开机完成之后再打开第二个屏幕，如果已经双屏幕开机产生花屏，可以关闭一个屏幕再打开
3. 不知道从哪个版本开始USB3出了问题，不能识别USB3设备，但是可以识别USB2设备，介意的就不要用这套驱动了

## 主要硬件

| 配置      | 型号                            |
| -------- | ------------------------------- |
| 主板      | 微星B460M MORTAR WIFI           |
| CPU      | i7-10700                        |
| 显卡      | 核显 UHD630                     |
| wifi 蓝牙 | 板载                            |
| 内存      | 2 x 32G 金士顿 DDR4 2666 骇客神条 |
| 显示器    | 2 x Redmi 23.8英寸              |
| 连接线    | 绿联 DP转HDMI转换器连接线          |
| 固态硬盘  | SAMSUNG 970 EVO 500G            |
| 机械硬盘  | 西数 紫盘 4TB                    |

## 驱动简介

```
EFI
├── BOOT
│   └── BOOTx64.efi
└── OC
    ├── ACPI ······························ DSDT补丁目录
    │   ├── SSDT-AWAC.aml ················· 时钟补丁
    │   ├── SSDT-EC-USBX.aml ·············· EC和USBX补丁
    │   ├── SSDT-PLUG.aml ················· 节能四项补丁
    │   ├── SSDT-PM.aml ··················· 节能五项补丁
    │   └── SSDT-RHUB.aml ················· 修复丢失的USB接口
    ├── Drivers
    │   ├── HfsPlus.efi
    │   ├── OpenCanopy.efi
    │   └── OpenRuntime.efi
    ├── Kexts ····························· 驱动目录
    │   ├── AirportItlwm.kext ············· 板载无线网卡
    │   ├── AppleALC.kext ················· 声卡
    │   ├── CtlnaAHCIPort.kext ············ 官方介绍建议使用，具体作用不清楚
    │   ├── IntelBluetoothFirmware.kext ··· 板载蓝牙，如果蓝牙开关不显示，加上IntelBluetoothInjector.kext
    │   ├── Lilu.kext ····················· 必备
    │   ├── LucyRTL8125Ethernet.kext ······ 有线网卡
    │   ├── NVMeFix.kext ·················· 提高非苹果SSD兼容性
    │   ├── SMCProcessor.kext ············· 监控CPU温度
    │   ├── SMCSuperIO.kext ··············· 监控风扇转速
    │   ├── USBMap.kext ··················· 手动创建的USB映射
    │   ├── VirtualSMC.kext ··············· 必备
    │   ├── WhateverGreen.kext ············ 必备
    ├── OpenCore.efi
    ├── Resources ························· 引导界面资源
    ├── Tools ····························· 引导界面工具
    │   ├── OpenShell.efi ················· 必备
    │   └── acpidump.efi ·················· 导出DSDT工具
    └── config.plist ······················ OpenCore配置文件
```

## 使用

安装或升级时会重启多次，不要慌，一步步来就行

参考下图修改`EFI/OC/config.plist`

![修改参数](https://raw.githubusercontent.com/xuelingkang/assets/master/hackintosh-opencore-mag-b460m-mortar-wifi-10700-uhd630-igpu/config.plist.png)

## 参考
[mrdonkey3/hackintosh-oc-msi-b460m-mortar-i7-10700-big-sur](https://github.com/mrdonkey3/hackintosh-oc-msi-b460m-mortar-i7-10700-big-sur)
> 一个配置类似的驱动，介绍详细且简单易懂，适合小白入手

[OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
> 官方说明书，耐心看，基本上能解决所有问题

