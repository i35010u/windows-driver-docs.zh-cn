---
title: 释放驱动程序分配的资源
description: 释放驱动程序分配的资源
ms.assetid: b286b4b0-54f2-4798-a77b-c08743502552
keywords:
- 卸载例程 WDK 内核，非 PnP 驱动程序
- 非即插即用卸载例程 WDK 内核
- 释放驱动程序分配资源
- 驱动程序分配资源释放 WDK 内核
- 资源释放 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578d93631f67edc7b566345d3eeda9f59db6b0d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373432"
---
# <a name="releasing-driver-allocated-resources"></a>释放驱动程序分配的资源





驱动程序如何使用注册表的详细信息，还设置了系统对象和在其设备扩展、 控制器扩展插件或驱动程序分配非分页缓冲的池的资源而异的驱动程序到驱动程序。 但是，任何[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程必须释放一个驱动程序使用分阶段的资源。

任何驱动程序*Unload*例程必须确保没有其他驱动程序例程当前正在使用，或可能很快就会使用特定的资源之前释放该资源。

一般情况下， *Unload*例程在以下几个阶段中释放所有驱动程序分配的资源：

1.  如果该驱动程序还未执行该操作，如果可能，请禁用任何物理设备上的中断，然后调用[ **IoDisconnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)立即中断处于禁用状态。

2.  确保没有其他驱动程序例程可以引用资源的*Unload*例程打算发布。

    例如， *Unload*例程必须调用[ **IoStopTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostoptimer)如果驱动程序的[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)特定设备对象当前已启用例程。 它必须确保没有线程正在等待的任何驱动程序的调度程序对象和其计时器对象不是排队等待调用其[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程之前释放用于存储其调度程序对象。 它必须调用[ **KeRemoveQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovequeuedpc)如果它具有[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程 ISR 可能已排入队列，依次类推。

    如果该驱动程序调用[ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)，必须确保已完成的工作项。 **IoQueueWorkItem**采用 out 关联的设备对象上的引用; 如果任何此类引用都保持不能卸载该驱动程序。

    如果该驱动程序调用[ **PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)，则*卸载*例程也必须导致驱动程序创建的线程会运行，以便该线程本身可以调用[ **PsTerminateSystemThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psterminatesystemthread)驱动程序卸载之前。 驱动程序无法释放驱动程序创建系统线程通过调用[ **ZwClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)与*ThreadHandle*返回的**PsCreateSystemThread**.

3.  释放该驱动程序分配的特定于设备的资源。 执行此操作可能涉及调用以下系统支持例程：
    -   [**IoDeleteSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletesymboliclink)如果[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)或者[*重新初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)例程调用[**IoCreateSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesymboliclink)或[ **IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreateunprotectedsymboliclink)，并且[ **IoDeassignArcName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeassignarcname)如果驱动程序调用[ **IoAssignArcName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioassignarcname)。

    -   [**ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)如果**DriverEntry**或驱动程序的任何其他例程调用[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)和驱动程序尚未发布已分配的内存。

    -   [**MmUnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)如果**DriverEntry**或*重新初始化*例程调用[ **MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)。

    -   [**MmFreeNonCachedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmfreenoncachedmemory)如果**DriverEntry**或*重新初始化*例程调用[ **MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmallocatenoncachedmemory).

    -   [**MmFreeContiguousMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreecontiguousmemory)如果**DriverEntry**或*重新初始化*例程调用[ **MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemory).

    -   [**FreeCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_common_buffer)如果**DriverEntry**或*重新初始化*例程调用[ **AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer).

    -   [**IoAssignResources** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)或[ **IoReportResourceUsage** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)如果**DriverEntry**或*重新初始化*这些例程调用的一个支持例程或[ **HalAssignSlotResources** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))为自身和/或其物理设备的声明配置注册表中的硬件资源单独。

4.  释放系统对象和资源的**DriverEntry**或*重新初始化*设备扩展的设备对象中或在控制器对象的控制器扩展中设置的例程 (如果它创建了一个）。 具体而言，该驱动程序必须执行以下操作之前它将尝试删除的设备对象 ([**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)) 或控制器对象 ([**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeletecontroller)):
    -   调用[ **IoDisconnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)来释放中断对象指针存储在相应的设备或控制器扩展。
    -   调用[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)如果它调用的下一步低驱动程序的文件对象的指针与[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)和 this 指针存储在扩展名为设备或控制器。
    -   调用[ **IoDetachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)具有较低的驱动程序的设备对象，如果它调用的指针[ **IoAttachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevice)或[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)和 this 指针存储在扩展名为设备或控制器。

5.  免费的硬件资源的**DriverEntry**或*重新初始化*例程声明的驱动程序的物理设备，如果有，注册表项下 **\\注册表\\机器\\硬件\\ResourceMap**树。

6.  删除其设备的任何名称， **DriverEntry**或*重新初始化*注册表中存储的例程 **\\注册表...\\DeviceMap**树，以及。

驱动程序已发布了设备、 系统和硬件资源后，它可以删除其设备和控制器的对象，如以下部分中所述。

 

 




