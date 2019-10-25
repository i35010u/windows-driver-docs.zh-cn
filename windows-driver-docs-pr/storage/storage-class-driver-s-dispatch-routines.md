---
title: 存储类驱动程序的调度例程
description: 存储类驱动程序的调度例程
ms.assetid: 99713661-5e99-4110-b369-afc084a2aaef
keywords:
- 调度例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f97249cbe3499cde4a7bfc26ebfe5de2f59e976
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845087"
---
# <a name="storage-class-drivers-dispatch-routines"></a>存储类驱动程序的调度例程


## <span id="ddk_storage_class_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DISPATCH_ROUTINES_KG"></span>


类驱动程序[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[**DispatchClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程通常没有特定于设备的要求。 大多数存储类驱动程序都是中间驱动程序;其调度例程只返回状态\_"成功" 以指示给定的设备对象存在，以便更高级别的驱动程序和、间接的用户模式应用程序可以打开设备进行 i/o 并在以后关闭设备。

类驱动程序[**DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[**DispatchInternalDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程必须是驻留的;也就是说，它们不能是可分页的，也不能是驱动程序的可分页图像部分。 根据给定请求的 IOCTL，此类调度例程可能会调用分页例程或等待来自同步或通知对象的调用（从而阻止执行线程），但调度例程必须能够通过传递未知的 IOCTL调度\_级别。

存储类驱动程序必须具有[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程，以便能够启动、停止和删除设备，并响应其他 PnP 请求，例如，通知设备在寻呼路径上。 有关处理 PnP 开始请求的详细信息，请参阅[在存储类驱动程序中处理 Pnp 启动](handling-pnp-start-in-a-storage-class-driver.md)。 有关处理其他 PnP 请求的详细信息，请参阅[处理对存储外围设备的 Pnp 请求](handling-pnp-requests-to-storage-peripherals.md)。

存储类驱动程序还必须具有[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程，请求设置其设备的电源状态。 有关详细信息，请参阅[处理存储外围设备的电源请求](handling-power-requests-to-storage-peripherals.md)。

如果存储类驱动程序的设备在内部缓存数据，则存储类驱动程序必须具有[**DispatchShutdown**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程，可能为[**DispatchFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程，如果其设备可能连接到由 HBA 缓存数据的总线驱动，或者文件系统分层在类驱动程序之上。 为了保持数据完整性，应在关闭系统前将此类缓存刷新到设备。

有关调度例程一般要求的详细信息，另请参阅[编写调度例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)。

 

 




