---
title: 存储类驱动程序的调度例程
description: 存储类驱动程序的调度例程
ms.assetid: 99713661-5e99-4110-b369-afc084a2aaef
keywords:
- 调度例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94aa348e89b8d6b88d1d49e81bbc281e42e4e935
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190943"
---
# <a name="storage-class-drivers-dispatch-routines"></a>存储类驱动程序的调度例程


## <span id="ddk_storage_class_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DISPATCH_ROUTINES_KG"></span>


类驱动程序 [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [**DispatchClose**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程通常没有特定于设备的要求。 大多数存储类驱动程序都是中间驱动程序;其调度例程只返回状态 " \_ 成功" 以指示给定的设备对象存在，以便更高级别的驱动程序和、间接、用户模式应用程序可以打开设备进行 i/o 并在以后关闭设备。

类驱动程序 [**DispatchDeviceControl**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [**DispatchInternalDeviceControl**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程必须是驻留的;也就是说，它们不能是可分页的，也不能是驱动程序的可分页图像部分。 根据给定请求的 IOCTL，此类调度例程可能会调用分页例程或等待来自同步或通知对象的调用 (从而阻止正在执行的线程) ，但是调度例程必须能够通过调度级别传递未知的 IOCTL \_ 。

存储类驱动程序必须具有 [**DispatchPnP**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程，以便能够启动、停止和删除设备，并响应其他 PnP 请求，例如，通知设备在寻呼路径上。 有关处理 PnP 开始请求的详细信息，请参阅 [在存储类驱动程序中处理 Pnp 启动](handling-pnp-start-in-a-storage-class-driver.md)。 有关处理其他 PnP 请求的详细信息，请参阅 [处理对存储外围设备的 Pnp 请求](handling-pnp-requests-to-storage-peripherals.md)。

存储类驱动程序还必须具有 [**DispatchPower**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程，请求设置其设备的电源状态。 有关详细信息，请参阅 [处理存储外围设备的电源请求](handling-power-requests-to-storage-peripherals.md)。

如果存储类驱动程序的设备可能已连接到由 HBA 缓存数据的总线，或者文件系统在类驱动程序之上，则存储类驱动程序必须具有 [**DispatchShutdown**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程，并且可能有 [**DispatchFlushBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程。 为了保持数据完整性，应在关闭系统前将此类缓存刷新到设备。

有关调度例程一般要求的详细信息，另请参阅 [编写调度例程](../kernel/writing-dispatch-routines.md) 。

 

