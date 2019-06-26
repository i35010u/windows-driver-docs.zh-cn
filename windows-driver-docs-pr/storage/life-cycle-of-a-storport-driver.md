---
title: Storport 驱动程序的生命周期
description: Storport 驱动程序的生命周期
ms.assetid: 6b48cf8e-83c3-4403-88fd-1bf1f285aafc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf527f2f5f3ccf02ed1461b7a2f024b9587183f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384164"
---
# <a name="life-cycle-of-a-storport-driver"></a>Storport 驱动程序的生命周期


到 Storport 驱动程序中的微型端口驱动程序，可以在回调例程方面描述 Storport 驱动程序的生命周期。 回调例程可以分为几个主要的组，如图 1 中所示。

![图演示总体 storport 体系结构](images/storport-1.png)

每种类型的回调例程的几个示例图 2 所示。 当在系统启动时和首次加载该驱动程序、 微型端口驱动程序**DriverEntry**调用例程。 此例程填写提供 Storport 微型端口驱动程序的入口点，也称为其回调例程或回调的数据结构。 接近此例程结束时，微型端口驱动程序调用[ **StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)。 Storport 驱动程序，然后调用微型端口回调例程[ **HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)，或在虚拟微型端口驱动程序的情况下[ **VirtualHwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-virtual_hw_find_adapter). 从该例程返回微型端口驱动程序的后[ **HwStorInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)调用例程。

Storport 然后获取微型端口驱动程序的支持的控件类型通过调用其[ **HwStorAdapterControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)例程替换**ScsiQuerySupportedControlTypes**为参数。

![图 2: storport 回调例程](images/storport-2.png)

主要 I/O 路径由一系列调用到[ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio) （在虚拟微型端口驱动程序的情况下除外） 和[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio). 有关详细信息，请参阅[未同步 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)。

当系统关闭时[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)调用使用类型 SRB SRB\_函数\_关闭。 当适配器被删除或禁用在运行时系统，或输入系统时休眠模式， [ **HwStorAdapterControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)使用调用**ScsiStopAdapter**作为参数。 从恢复系统时休眠模式， **HwStorAdapterControl**使用调用**ScsiRestartAdapter**作为参数。

 

 




