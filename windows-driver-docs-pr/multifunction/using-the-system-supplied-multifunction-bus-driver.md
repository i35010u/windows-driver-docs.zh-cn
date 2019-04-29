---
title: 使用系统提供的多功能总线驱动程序
description: 使用系统提供的多功能总线驱动程序
ms.assetid: 75fe659d-5311-4bc6-adfb-fd608e10c718
keywords:
- 多功能设备 WDK，系统提供的总线驱动程序
- 系统提供多功能总线驱动程序 WDK
- mf.sys
- 功能的设备对象 WDK 的多功能设备
- FDOs WDK 多功能设备
- 物理设备对象 WDK 多功能设备
- PDOs WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94f9cbdb5f0fd1e6eed1785b5149344b804f0793
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379595"
---
# <a name="using-the-system-supplied-multifunction-bus-driver"></a>使用系统提供的多功能总线驱动程序





如果设备的基础总线支持一种多功能总线标准，如 PC 卡、 一个基于 NT 的平台上的多功能设备的供应商可以使用系统提供多功能总线驱动程序 (mf.sys) 支持的设备。

Mf.sys 总线驱动程序句柄 PnP 设备功能的枚举，并且仲裁函数之间的资源，如 I/O 端口和 Irq。 Mf.sys 驱动程序管理父多功能设备的电源处理子函数的电源管理。

若要使用 mf.sys，多功能设备必须满足以下要求：

-   设备的基础 bus 必须具有一个多功能标准。

-   [**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)的子函数必须相同，而且必须与父设备的相匹配。 查询的子函数的设备功能时 ([**IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664))，mf.sys 驱动程序报告的设备功能父设备中。

-   为多功能设备所在，例如 pcmcia.sys，总线驱动程序必须处理任何[ **IRP\_MN\_读取\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)和[**IRP\_MN\_编写\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551769)请求。 Mf.sys 驱动程序只需将这些 Irp 传递给父总线驱动程序。

-   必须是独立的函数： 它们不能具有启动顺序的依赖项，不能以另一个函数 （例如，function1 使用 I/O 端口 X 和 function2 使用 portX + 200）; 的资源表示一个函数的资源要求和每个函数必须能够充当一个单独的设备，即使它由与另一个函数相同的驱动程序提供服务。

若要使用 mf.sys，供应商提供的多功能设备的设备的驱动程序为指定 mf.sys INF。 如果设备完整、 准确地满足其基础的总线的标准多功能，此类设备的供应商可以使用系统提供 mf.inf。 如果设备不完全符合标准，供应商必须提供自定义 INF。

在任一情况下，由供应商还提供驱动程序和设备上的各个函数的 INF 文件。

自定义的多功能 INF 以下框架演示了用于指定 mf.sys 作为多功能设备的驱动程序所需的语法：

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

请考虑组合 LAN/调制解调器 PC 卡设备。 如果没有任何特殊的多功能支持，此类设备可能 PCMCIA 总线驱动程序报告为单个调制解调器设备。 多功能 INF 和 mf.sys 总线驱动程序的额外支持下，枚举设备的这两个函数。 下图显示了可能会为此类组合 PC 卡与所需的多功能支持创建的示例设备堆栈。

![说明通过 mf.sys 枚举的多功能设备的设备堆栈的关系图](images/mf-layers.png)

如中所示上图中，为总线驱动程序上驻留的多功能设备枚举一台设备。 多功能的 INF 文件中的硬件 ID 将导致 PnP 管理器中，以作为设备的功能驱动程序加载 mf.sys 总线驱动程序。 Mf.sys 总线驱动程序枚举两个子设备、 LAN 设备和调制解调器。

即插即用的管理器会将典型的设备，如每个子设备查找 INF 文件加载适当的驱动程序调用其 AddDevice 例程，依次类推，直到为每个设备创建设备堆栈。 Mf.sys 总线驱动程序进行仲裁子设备的资源，并管理设备的任何其他多功能方面。 就像它们是不同的设备，多功能卡供应商提供了多种功能 （LAN 和调制解调器） 功能的驱动程序和 Inf。

图重点介绍功能的驱动程序和父总线驱动程序及其关联 FDOs 和 PDOs。 任何筛选器驱动程序 （和筛选器 DOs） 为简单起见，省略了。

 

 




