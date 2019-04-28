---
title: Storport 驱动程序的生命周期
description: Storport 驱动程序的生命周期
ms.assetid: 6b48cf8e-83c3-4403-88fd-1bf1f285aafc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74266fa57d7663c70cbd1e8b0ddec100c1cbdcd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355631"
---
# <a name="life-cycle-of-a-storport-driver"></a>Storport 驱动程序的生命周期


到 Storport 驱动程序中的微型端口驱动程序，可以在回调例程方面描述 Storport 驱动程序的生命周期。 回调例程可以分为几个主要的组，如图 1 中所示。

![图演示总体 storport 体系结构](images/storport-1.png)

每种类型的回调例程的几个示例图 2 所示。 当在系统启动时和首次加载该驱动程序、 微型端口驱动程序**DriverEntry**调用例程。 此例程填写提供 Storport 微型端口驱动程序的入口点，也称为其回调例程或回调的数据结构。 接近此例程结束时，微型端口驱动程序调用[ **StorPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff567108)。 Storport 驱动程序，然后调用微型端口回调例程[ **HwStorFindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff557390)，或在虚拟微型端口驱动程序的情况下[ **VirtualHwStorFindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff568008). 从该例程返回微型端口驱动程序的后[ **HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396)调用例程。

Storport 然后获取微型端口驱动程序的支持的控件类型通过调用其[ **HwStorAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557365)例程替换**ScsiQuerySupportedControlTypes**为参数。

![图 2: storport 回调例程](images/storport-2.png)

主要 I/O 路径由一系列调用到[ **HwStorBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557369) （在虚拟微型端口驱动程序的情况下除外） 和[ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423). 有关详细信息，请参阅[未同步 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)。

当系统关闭时[ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423)调用使用类型 SRB SRB\_函数\_关闭。 当适配器被删除或禁用在运行时系统，或输入系统时休眠模式， [ **HwStorAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557365)使用调用**ScsiStopAdapter**作为参数。 从恢复系统时休眠模式， **HwStorAdapterControl**使用调用**ScsiRestartAdapter**作为参数。

 

 




