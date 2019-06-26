---
title: 支持具有不完整配置寄存器的电脑卡
description: 支持具有不完整配置寄存器的电脑卡
ms.assetid: 62bdb1e7-ca45-42e6-bdf5-c48fb3ddb3fc
keywords:
- 不完整的配置将 WDK 多功能设备注册
- 系统提供多功能总线驱动程序 WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b31395f4e87edbe4336d52128dd93bea3086e1ff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386377"
---
# <a name="supporting-pc-cards-that-have-incomplete-configuration-registers"></a>支持具有不完整配置寄存器的电脑卡





如果多功能的 16 位 PC 卡设备不具有配置为每个函数的寄存器，此类设备的供应商可以使用系统提供多功能总线驱动程序 (mf.sys)，但必须提供各个函数的自定义的 INF 文件和支持。

在基于 NT 的平台上的此类设备的供应商可以使用系统提供的以下组件：

-   多功能设备的函数驱动程序。 （系统提供）

    自定义设备 INF 必须指定 mf.sys 作为设备的功能驱动程序。 然后，系统提供 mf.sys 驱动程序将枚举设备的功能。

    请参阅[使用 System-Supplied 多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md)有关使用系统提供 mf.sys 驱动程序详细信息。

此类设备的供应商必须提供以下信息：

-   多功能设备的自定义 INF 文件。 （供应商提供）

    供应商必须提供一个多功能的 INF 文件作为多功能总线驱动程序指定 mf.sys，指定的类"多功能"（使用其关联的 GUID 作为在定义 devguid.h)，并提供缺少的配置注册信息。 查看更多更高版本在本部分中的信息。

-   每个函数的设备的即插即用功能驱动程序。 （供应商提供）

    由于多功能总线驱动程序处理的多功能语义，功能的驱动程序可以是函数打包为单个设备时使用了相同驱动程序。

-   用于设备的每个函数的 INF 文件。 （供应商提供）

    INF 文件可以是函数打包为单个设备时，将使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

在此类设备供应商提供的自定义 INF 必须指定：

-   mf.sys 作为设备的服务。

    请参阅[使用 System-Supplied 多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md)有关详细信息。

-   多功能设备的资源要求。

    指定在资源需求[ **INF DDInstall.LogConfigOverride 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)。

-   设备的每个函数的硬件 ID。

    指定在硬件 Id [ **INF DDInstall.HW 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。

-   资源的设备，用于标识每个子函数所需的父资源的每个函数映射。

    指定资源映射中 INF *DDInstall*。**HW**部分。 请参阅[创建资源将映射为多功能设备](creating-resource-maps-for-a-multifunction-device.md)有关创建资源的详细信息将映射。

INF 必须重新提出所指定的设备，因为 INF 中存在替代配置时，如果 PnP 管理器不使用该设备从任何设备资源要求的所有资源要求。

对于此类设备，配置选项注册可以通过编程使用**PcCardConfig**类似编程单函数设备条目。 **PcCardConfig**条目包含适用于整个设备的信息。 **PcCardConfig**中记录条目[ **INF LogConfig 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-logconfig-directive)。

指定时**PcCardConfig**多功能设备的格式项*ConfigIndex*为单函数设备定义的相同。 配置注册单函数 PC 卡包含一组资源在该设备的属性中定义的索引。 此指令还可以用于使用基于索引的格式的配置选项注册某些多功能设备。

下面的示例显示了用于安装多功能设备作为其总线驱动程序使用 mf.sys 并具有不完整的配置寄存器的 INF 文件。

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

INF，如以上副本 ID 和资源信息对注册表的子函数所示。 当枚举设备的子函数时，mf.sys 驱动程序从注册表检索的信息。








