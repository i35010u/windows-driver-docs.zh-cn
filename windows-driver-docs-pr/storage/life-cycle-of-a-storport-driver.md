---
title: Storport 驱动程序的生命周期
description: Storport 驱动程序的生命周期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f241954e100ac43544cce1d5793a6056779a6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811607"
---
# <a name="life-cycle-of-a-storport-driver"></a>Storport 驱动程序的生命周期


Storport 驱动程序的生命周期可以从 Storport 驱动程序中的回小型驱动程序中的回调例程进行描述。 回调例程可以分为多个主要组，如图1所示。

![阐释总体 storport 体系结构的图](images/storport-1.png)

图2显示了每种类型的回调例程的几个示例。 系统启动并且第一次加载驱动程序时，将调用微型端口驱动程序的 **DriverEntry** 例程。 此例程使用微型端口驱动程序的入口点（也称为其回调例程或回调）来填充提供 Storport 的数据结构。 在此例程结束时，微型端口驱动程序调用 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)。 Storport 驱动程序接着调用微型端口回调例程 [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)，或者在虚拟微型端口驱动程序 [**VirtualHwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter)的情况下调用。 从该例程返回后，将调用微型端口驱动程序的 [**HwStorInitialize**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize) 例程。

然后，通过将 **ScsiQuerySupportedControlTypes** 作为参数调用，来获取微型端口 [**HwStorAdapterControl**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)驱动程序的受支持的控件类型。

![图2： storport 回调例程](images/storport-2.png)

主 i/o 路径包含一系列对 [**HwStorBuildIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) (的调用，在虚拟微型端口驱动程序) 和 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)的情况下除外。 有关详细信息，请参阅未 [同步的 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)。

关闭系统后，将使用 SRB 函数关闭类型的 SRB 调用 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) \_ \_ 。 当系统正在运行或系统正在运行时，或当系统进入休眠模式时，将使用 **ScsiStopAdapter** 作为参数调用 [**HwStorAdapterControl**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control) 。 当系统从休眠模式恢复时，将使用 **ScsiRestartAdapter** 作为参数调用 **HwStorAdapterControl** 。

 

