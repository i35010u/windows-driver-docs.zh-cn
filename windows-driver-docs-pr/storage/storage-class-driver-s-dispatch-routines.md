---
title: 存储类驱动程序的调度例程
description: 存储类驱动程序的调度例程
ms.assetid: 99713661-5e99-4110-b369-afc084a2aaef
keywords:
- 调度例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ba40f2b2ff09c5be8ae7b4961140b16a5c982f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368218"
---
# <a name="storage-class-drivers-dispatch-routines"></a>存储类驱动程序的调度例程


## <span id="ddk_storage_class_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DISPATCH_ROUTINES_KG"></span>


类驱动程序[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ **DispatchClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程通常具有任何特定于设备的要求。 大多数存储类驱动程序是中间驱动程序;其调度例程仅返回状态\_成功，指示给定的设备对象存在，以便更高级别的驱动程序和用户模式应用程序，间接地，可以为 I/O 打开设备并之后关闭设备。

类驱动程序[ **DispatchDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ **DispatchInternalDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须驻留; 也就是说，它们不能为可分页，也不属于驱动程序的可分页图像部分。 根据给定请求的 IOCTL，此类的调度例程可能会调用分页的例程或等待调用同步或通知对象 （从而阻止正在执行的线程），但调度例程必须能够传递通过未知的 IOCTL在调度\_级别。

存储类驱动程序必须具有[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程的请求，若要开始，停止和中删除该设备和设备是分页路径的通知等其他即插即用请求响应。 有关处理即插即用启动请求的详细信息，请参阅[存储类驱动程序中处理即插即用启动](handling-pnp-start-in-a-storage-class-driver.md)。 有关处理其他即插即用的请求的详细信息，请参阅[处理与存储外围设备的即插即用请求](handling-pnp-requests-to-storage-peripherals.md)。

存储类驱动程序还必须具有[ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程的请求，若要设置其设备的电源状态。 有关详细信息，请参阅[处理与存储外围设备的电源请求](handling-power-requests-to-storage-peripherals.md)。

存储类驱动程序必须具有[ **DispatchShutdown** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程和可能[ **DispatchFlushBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程如果其设备在内部，缓存数据，如果其设备可能连接到总线由在内部，缓存数据的 HBA 驱动或文件系统上的类驱动程序进行分层。 为了维护数据完整性，应将此类缓存刷新到设备之前在系统关闭的情况下。

另请参阅[写入调度例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)调度例程的常规要求有关的详细信息。

 

 




