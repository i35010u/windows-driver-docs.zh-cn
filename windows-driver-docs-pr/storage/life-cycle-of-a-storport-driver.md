---
title: Storport 驱动程序的生命周期
description: Storport 驱动程序的生命周期
ms.assetid: 6b48cf8e-83c3-4403-88fd-1bf1f285aafc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77430baf44731f93741bdba1c493ede07f42a662
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841623"
---
# <a name="life-cycle-of-a-storport-driver"></a>Storport 驱动程序的生命周期


Storport 驱动程序的生命周期可以从 Storport 驱动程序中的回小型驱动程序中的回调例程进行描述。 回调例程可以分为多个主要组，如图1所示。

![阐释总体 storport 体系结构的图](images/storport-1.png)

图2显示了每种类型的回调例程的几个示例。 系统启动并且第一次加载驱动程序时，将调用微型端口驱动程序的**DriverEntry**例程。 此例程使用微型端口驱动程序的入口点（也称为其回调例程或回调）来填充提供 Storport 的数据结构。 在此例程结束时，微型端口驱动程序调用[**StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)。 Storport 驱动程序接着调用微型端口回调例程[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)，或者在虚拟微型端口驱动程序[**VirtualHwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter)的情况下调用。 从该例程返回后，将调用微型端口驱动程序的[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)例程。

然后，通过将**ScsiQuerySupportedControlTypes**作为参数调用，来获取微型端口[](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)驱动程序的受支持的控件类型。

![图2： storport 回调例程](images/storport-2.png)

主 i/o 路径由一系列对[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) （虚拟微型端口驱动程序除外）和[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)的调用组成。 有关详细信息，请参阅未[同步的 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)。

关闭系统后，将使用 SRB 类型的 SRB 调用[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) ，\_函数\_关闭。 当系统正在运行或系统正在运行时，或当系统进入休眠模式时，将使用**ScsiStopAdapter**作为参数调用[**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control) 。 当系统从休眠模式恢复时，将使用**ScsiRestartAdapter**作为参数调用**HwStorAdapterControl** 。

 

 




