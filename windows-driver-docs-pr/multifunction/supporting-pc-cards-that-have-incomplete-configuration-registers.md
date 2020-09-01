---
title: 支持具有不完整配置寄存器的电脑卡
description: 支持具有不完整配置寄存器的电脑卡
ms.assetid: 62bdb1e7-ca45-42e6-bdf5-c48fb3ddb3fc
keywords:
- 不完整的配置注册 WDK 多功能设备
- 系统提供的多功能总线驱动程序 WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 130d76a9cd80fc75337e99a2a9efc3031e0477b8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190949"
---
# <a name="supporting-pc-cards-that-have-incomplete-configuration-registers"></a>支持具有不完整配置寄存器的电脑卡





如果多功能16位 PC 卡设备没有适用于每个功能的配置寄存器，此类设备的供应商可以使用系统提供的多功能总线驱动程序 ( # A0) ，但必须提供自定义 INF 文件并支持单个功能。

此类设备在基于 NT 的平台上的供应商可以使用以下系统提供的组件：

-   多功能设备的函数驱动程序。  (系统提供的) 

    设备的自定义 INF 必须指定 mf.sys 作为设备的函数驱动程序。 系统提供的 mf.sys 驱动程序将枚举设备的功能。

    有关使用系统提供的 mf.sys 驱动程序的详细信息，请参阅 [使用系统提供的多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md) 。

此类设备的供应商必须提供以下各项：

-   多功能设备的自定义 INF 文件。  (供应商提供的) 

    供应商必须提供将 mf.sys 指定为多功能总线驱动程序的多功能 INF 文件，指定类 "多功能" (及其关联 GUID （如 devguid) 中所定义），并提供缺少的配置寄存器信息。 请参阅本节后面部分的详细信息。

-   设备的每个功能的 PnP 函数驱动程序。  (供应商提供的) 

    由于多功能总线驱动程序处理多功能语义，因此函数驱动程序可以是将函数打包为单个设备时使用的相同驱动程序。

-   设备的每个功能的 INF 文件。  (供应商提供的) 

    INF 文件可以是在将函数打包为单个设备时使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

供应商提供的此类设备的自定义 INF 必须指定：

-   作为设备的服务 mf.sys。

    有关详细信息，请参阅 [使用系统提供的多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md) 。

-   多功能设备的资源要求。

    指定 [**INF DDInstall. LogConfigOverride 部分**](../install/inf-ddinstall-logconfigoverride-section.md)中的资源要求。

-   设备的每个功能的硬件 ID。

    在 [**INF DDInstall 部分**](../install/inf-ddinstall-hw-section.md)中指定硬件 id。

-   设备的每个函数的资源映射，标识每个子函数所需的父资源。

    在 INF *DDInstall*中指定资源映射。**HW** 部分。 有关创建资源映射的详细信息，请参阅 [创建多功能设备的资源图](creating-resource-maps-for-a-multifunction-device.md) 。

INF 必须重述设备指定的所有资源要求，因为如果 INF 中存在替代配置，则 PnP 管理器不会使用设备提供的任何设备资源要求。

对于这种设备，可以使用 **PcCardConfig** 条目来编程配置选项 register，类似于对单功能设备进行编程。 **PcCardConfig**项包含适用于整个设备的信息。 **PcCardConfig**条目记录在[**INF LogConfig 指令**](../install/inf-logconfig-directive.md)中。

为多功能设备指定 **PcCardConfig** 条目时， *ConfigIndex* 的格式与为单功能设备定义的格式相同。 单功能 PC 卡的配置注册包含对该设备的属性中定义的一组资源的索引。 此指令还可用于使用配置选项注册的基于索引格式的某些设备设备。

下面的示例演示了一个 INF 文件，用于安装使用 mf.sys 作为其总线驱动程序的多功能设备，并且具有不完整的配置寄存器。

```cpp
; MFSupra.inf
; This file installs the Supra Dual 56K modem
; Copyright 1999 Microsoft Corporation

[version]
Signature  = "$Windows NT$"
provider   = %MSFT%
Class      = MultiFunction              ; system-defined class
ClassGUID  = {4d36e971-e325-11ce-bfc1-08002be10318}

[ControlFlags]
ExcludeFromSelect=*SUP2440  ; don't include PnP devices in lists of
                            ; devices to be manually installed

[Manufacturer]
%M_Supra% = Supra

[Supra]
%Supra1% = Sup2231GoCard.mf, *SUP2440 

[Sup2231GoCard.mf.NT]
Include = mf.inf           ; specify that this device needs mf.sys
Needs = MFINSTALL.mf

[Sup2231GoCard.mf.NT.HW]
AddReg=Sup2231.mf.RegHW

[Sup2231.mf.RegHW]   
HKR, Child0000, HardwareID,  ,  MF\Shotgun_DEV0  ;modem1
HKR,Child0000,ResourceMap,1,00,02
HKR, Child0001, HardwareID,  ,  MF\Shotgun_DEV1  ;modem2
HKR,Child0001,ResourceMap,1,01,02

[Sup2231GoCard.mf.NT.Services]   
Include = mf.inf
Needs = MFINSTALL.mf.Services

[Sup2231GoCard.mf.NT.LogConfigOverride]   
LogConfig = Sup223x.mf.Override0, Sup223x.mf.Override1, \
 Sup223x.mf.Override2, Sup223x.mf.Override3

[Sup223x.mf.Override0]
ConfigPriority = NORMAL
IOConfig     = 2F8-2FF                  ; Com2
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ    
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 59(W)                    ; ConfigIndex

[Sup223x.mf.Override1]
ConfigPriority = NORMAL
IOConfig     = 3E8-3EF                  ; Com3
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ    
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 69(W)                    ; ConfigIndex

[Sup223x.mf.Override2]
ConfigPriority = NORMAL
IOConfig     = 2E8-2EF                  ; Com4
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ    
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 79(W)                    ; ConfigIndex

[Sup223x.mf.Override3]
ConfigPriority = NORMAL
IOConfig     = 3F8-3FF                  ; Com1
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 49(W)                    ; ConfigIndex

[strings]
MSFT = "Microsoft"
M_Supra = "Supra"
Supra1 = "Supra Dual 56K modem"
```

类似于上面所示的 INF 将子函数的 ID 和资源信息复制到注册表。 mf.sys 驱动程序在枚举设备的子函数时，从注册表中检索信息。