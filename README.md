# 微星B460M MORTAR WIFI i7-10700 核显 黑苹果 OpenCore驱动

## 系统信息

| MacOS            | OpenCore |
|------------------|----------|
| Catalina 10.15.7 | 0.6.6    |
| Big Sur 11.6.5   | 0.8.0    |
| Monterey 12.3.1  | 0.8.0    |

Monterey问题：

- DP转HDMI输出无信号
- DP转VGA输出正常，应该是模拟信号的原因，细看有点虚
- DP和HDMI输出正常

可用功能：以太网、wifi、蓝牙、USB映射、节能五项。。。

遗留问题：

1. 关机后自动重启，解决办法：在BIOS禁用USB唤醒，路径：Settings/Advanced/Wake Up Event Setup/Resume By USB Device，这样会产生另一个问题，鼠标和键盘无法唤醒，但是可以使用电源键唤醒。希望有更优方案的大神分享一下
2. 双屏幕开机会花屏，解决办法：单屏幕开机完成之后再打开第二个屏幕，如果已经双屏幕开机产生花屏，可以关闭一个屏幕再打开
3. 搬运了大佬的XHCI-unsupported.kext，解决了USB3接口不识别USB3设备的问题，虽然可以用了，但是速度和USB2一样

## 主要硬件

| 配置       | 型号                                                                       |
|-----------|----------------------------------------------------------------------------|
| 主板       | 微星B460M MORTAR WIFI                                                      |
| CPU       | i7-10700                                                                   |
| 显卡       | 核显 UHD630                                                                |
| wifi 蓝牙  | 板载                                                                       |
| 内存       | 2 x 32G 金士顿 DDR4 2666 骇客神条                                            |
| 显示器     | 2 x Redmi 23.8英寸                                                          |
| 连接线1    | 显示器原装HDMI线                                                             |
| 连接线2    | 绿联 DP转HDMI（公对母） + 显示器原装HDMI线<br>绿联 DP转VGA（公对公，Monterey用这条）|
| 固态硬盘   | SAMSUNG 970 EVO 500G                                                        |
| 机械硬盘   | 西数 紫盘 4TB                                                                |

## 驱动简介

```
EFI
├── BOOT
│   └── BOOTx64.efi
└── OC
    ├── ACPI ······························ DSDT补丁目录
    │   ├── SSDT-AWAC.aml ················· 时钟补丁
    │   ├── SSDT-EC-USBX.aml ·············· EC和USBX补丁
    │   ├── SSDT-PLUG.aml ················· 节能四项补丁
    │   ├── SSDT-PM.aml ··················· 节能五项补丁
    │   └── SSDT-RHUB.aml ················· 修复丢失的USB接口
    ├── Drivers
    │   ├── HfsPlus.efi
    │   ├── OpenCanopy.efi
    │   └── OpenRuntime.efi
    ├── Kexts ····························· 驱动目录
    │   ├── AirportItlwm.kext ············· 板载无线网卡
    │   ├── AppleALC.kext ················· 声卡
    │   ├── CtlnaAHCIPort.kext ············ 对于Big Sur，代替SATA-unsupported.kext，增加对各种SATA控制器的支持
    │   ├── IntelBluetoothFirmware.kext ··· 板载蓝牙固件
    │   ├── IntelBluetoothInjector.kext ··· 支持蓝牙开关
    │   ├── Lilu.kext ····················· 必备
    │   ├── LucyRTL8125Ethernet.kext ······ 有线网卡
    │   ├── NVMeFix.kext ·················· 提高非苹果SSD兼容性
    │   ├── SMCProcessor.kext ············· 监控CPU温度
    │   ├── SMCSuperIO.kext ··············· 监控风扇转速
    │   ├── USBMap.kext ··················· 手动创建的USB映射
    │   ├── VirtualSMC.kext ··············· 必备
    │   ├── WhateverGreen.kext ············ 必备
    │   └── XHCI-unsupported.kext ········· 非原生USB控制器，官网说B460不需要，实际上，不加这个驱动就会出现USB3接口不识别USB3设备的问题
    ├── OpenCore.efi
    ├── Resources ························· 引导界面资源
    ├── Tools ····························· 引导界面工具
    │   └── OpenShell.efi ················· 必备
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

[黑苹果之我跳船了：为何弃用华擎B460M，改换微星迫击炮B460M WIFI](https://post.smzdm.com/p/adwn892k/)
> 搬运了这个大佬的修改的驱动：XHCI-unsupported.kext

