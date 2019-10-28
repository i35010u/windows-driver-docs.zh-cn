---
title: 使用系统提供的多功能总线驱动程序
description: 使用系统提供的多功能总线驱动程序
ms.assetid: 75fe659d-5311-4bc6-adfb-fd608e10c718
keywords:
- 多功能设备 WDK，系统提供的总线驱动程序
- 系统提供的多功能总线驱动程序 WDK
- mf
- 功能设备对象 WDK 多功能设备
- FDOs WDK 多功能设备
- 物理设备对象 WDK 多功能设备
- PDOs WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28c2043a74e8a5f801814a6ca5d5ace827f76484
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838288"
---
# <a name="using-the-system-supplied-multifunction-bus-driver"></a>使用系统提供的多功能总线驱动程序





如果设备的基础总线支持多功能总线标准（如 PC 卡），则基于 NT 的平台上的多功能设备供应商可以使用系统提供的多功能总线驱动程序（mf）来支持设备。

Mf 的 sys.databases 总线驱动程序处理函数之间的设备函数和仲裁资源（如 i/o 端口和 Irq）的 PnP 枚举。 Mf 驱动程序通过电源管理父多功能设备来处理子功能的电源管理。

若要使用 mf，多功能设备必须满足以下要求：

-   设备的基础总线必须具有多功能标准。

-   [**设备\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)子函数的功能必须相同，并且必须与父设备的功能匹配。 当查询子函数的设备功能（[**IRP\_MN\_QUERY\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)）时，mf 驱动程序将报告父设备的设备功能。

-   多功能设备所在的总线的驱动程序（如 MN）必须处理任何[**IRP\_\_读取\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)和[**IRP\_MN\_写入\_配置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)请求。 Mf 驱动程序只是将这些 Irp 传递到父总线驱动程序。

-   函数必须是独立的：它们不能具有开始顺序依赖项;一个函数的资源要求不能用另一个函数的资源来表示（例如，function1 使用 i/o 端口 X，function2 使用 portX + 200）;而且，每个函数都必须能够作为单独的设备运行，即使它是由另一个功能的同一驱动程序提供服务的。

若要使用 mf，供应商需要为多功能设备提供一个 INF，该设备将 mf 指定为设备的驱动程序。 如果设备完全且准确地符合底层总线的多功能标准，此类设备的供应商可以使用系统提供的 mf。 如果设备未完全符合标准，则供应商必须提供自定义 INF。

在任一情况下，供应商还为设备上的各个功能提供驱动程序和 INF 文件。

自定义多功能 INF 的以下主干说明了指定 mf 作为多功能设备驱动程序所需的语法：

```cpp
[Version]
Signature = "$Windows NT$"
; ...
Class = Multifunction   ; the system-defined class for MF devices
ClassGUID  = {4d36e971-e325-11ce-bfc1-08002be10318} ; GUID for MF
; ...
; ...
[ControlFlags]
ExcludeFromSelect = *   ; don't include PnP devices in a displayed list of 
                        ; devices available for manual installation
[Manufacturer]
; ...
; ...
[ModelsSection]         ; models section
; ...
; ...
[DDInstall.NT]          ; install section
Include = mf.inf        ; specify that this device requires mf.sys
Needs = MFINSTALL.mf
; ...
 
[DDinstall.NT.Services]
Include = mf.inf
Needs = MFINSTALL.mf.Services

[DDInstall.NT.HW]
AddReg=DDInstall.RegHW
 
[DDInstall.RegHW]
; put entries with child function hardware IDs here
; ...
 
; put override sections here...
; ...
 
[Strings]
; ...
```

请考虑将 LAN/调制解调器 PC 卡设备组合在一起。 如果没有任何特殊的多功能支持，PCMCIA 总线驱动程序可能会将此类设备报告为单一调制解调器设备。 随着多功能 INF 和 mf 的 mf 总线驱动程序的额外支持，会枚举设备的两个功能。 下图显示了可能为具有所需的多功能支持的组合 PC 卡创建的示例设备堆栈。

![说明 mf 所枚举的多功能设备的设备堆栈的关系图](images/mf-layers.png)

如上图所示，多功能设备所在的总线的驱动程序将枚举一个设备。 多功能 INF 文件中的硬件 ID 导致 PnP 管理器加载 mf 总线驱动程序作为设备的函数驱动程序。 Mf bus 驱动程序枚举两个子设备，即 LAN 设备和调制解调器。

PnP 管理器会将每个子设备（如典型设备）、查找 INF 文件、加载相应的驱动程序、调用其 AddDevice 例程等进行处理，直到为每个设备创建了一个设备堆栈。 Mf 的 sys.databases 总线驱动程序仲裁子设备的资源，并管理设备的任何其他多功能。 多功能卡的供应商为多个功能（LAN 和调制解调器）提供了函数驱动程序和 Inf，就像它们是单独的设备一样。

该图重点介绍函数驱动程序和父总线驱动程序及其关联的 FDOs 和 PDOs。 为简单起见，将省略任何筛选器驱动程序（和筛选器 DOs）。

 

 




