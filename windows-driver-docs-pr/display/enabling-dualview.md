---
title: 启用 DualView
description: 启用 DualView
ms.assetid: 7779c74d-2076-419d-94e4-07c36501524e
keywords:
- 双视图 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2349d4d1de591ec33c5d467de81b073779590a95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382340"
---
# <a name="enabling-dualview"></a>启用 DualView


## <span id="ddk_enabling_dualview_gg"></span><span id="DDK_ENABLING_DUALVIEW_GG"></span>


为最小的双视图实现，请执行以下操作：

-   微型端口驱动程序的前[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)返回时，调用新的视频端口驱动程序入口点[ **VideoPortCreateSecondaryDisplay**](https://msdn.microsoft.com/library/windows/hardware/ff570288)，以便生成适用于辅助视图的设备扩展。 在辅助设备扩展中，将添加两个新的私有成员：

    1.  一个标志，指示设备扩展适用的辅助显示器
    2.  一个指针，它包含主显示器的设备扩展的地址
-   必须在微型端口驱动程序进行四个更改[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)回调例程，修改响应所示的四个 IOCTL 请求的方式。 以下列表中的第四个项提供了两种方法来完成相同的结果。

    1.  以响应[ **IOCTL\_视频\_映射\_视频\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff567812)请求、 每个视图的帧缓冲区指针和长度应正确设置。
    2.  为响应[ **IOCTL\_视频\_设置\_当前\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff567846)请求应该对特定辅助视图。
    3.  为响应[ **IOCTL\_视频\_重置\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff567834)请求取决于该设备是主或辅助显示器。 如果该设备是主显示器，执行任何所需的操作。 如果设备处于辅助显示器，但是，建议不采取任何操作。
    4.  更改的响应[ **IOCTL\_视频\_共享\_视频\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff568149)请求，以获取正确的地图这两个视图。 请注意，对于 DirectDraw 实现，可以修改 DirectDraw 函数[ *DdMapMemory* ](https://msdn.microsoft.com/library/windows/hardware/ff549641)若要获取正确的地图，这两个视图。
-   显示驱动程序应注意逻辑帧缓冲区地址和物理的视频内存偏移量之间调整。 这是对于 DirectDraw 实现，尤其重要，因为在双视图主图面可能启动任意位置以外的内存位置 0。 显示驱动程序应通过填充通知 DirectDraw **pHalInfo-&gt;vmiData.pvPrimary**并**pHalInfo-&gt;vmiData.fpPrimary**具有相应的视频内存偏移量有关处理[ **DrvGetDirectDrawInfo**](https://msdn.microsoft.com/library/windows/hardware/ff556229)。

### <a name="span-idadditionalimplementationnotesspanspan-idadditionalimplementationnotesspanspan-idadditionalimplementationnotesspanadditional-implementation-notes"></a><span id="Additional_Implementation_Notes"></span><span id="additional_implementation_notes"></span><span id="ADDITIONAL_IMPLEMENTATION_NOTES"></span>其他实现说明

-   [*HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)只调用一次的主要设备对象。 必须在此调用中初始化辅助设备的任何对象。

-   有关[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178)在其中调用*bEnable*设置为**FALSE**，微型端口驱动程序应检查的其他视图状态。 它应避免关闭视频芯片，而其他视图是仍处于活动状态。

-   绝不能假定绘制操作具有相同的绘图上下文 （例如，颜色深度和跨距）。 这一点尤其重要的使用磁贴帧缓冲区的芯片。

-   GDI 只能设置内置设备上的主视图。 某些系统中的，如便携式计算机具有内置监视设备 (LCDs)，但也可以连接到外部监视器。 微型端口驱动程序应通过传递视频标记的视图中作为可移动\_视屏\_REMOVABLE 标志时，它调用[ **VideoPortCreateSecondaryDisplay**](https://msdn.microsoft.com/library/windows/hardware/ff570288)。

-   在双视图模式中的便携式计算机，应禁用热键开关。 在视频启用 ACPI 的系统上，微型端口驱动程序应拒绝[ **IOCTL\_视频\_VALIDATE\_子\_状态\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff568156)请求。

-   为便携式计算机支持 multichild 设备微型端口驱动程序应处理[ **IOCTL\_视频\_获取\_子\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567801)请求和返回的逻辑子关系 （在下一节中讨论）。

 

 





