---
title: 释放驱动程序分配的资源
description: 释放驱动程序分配的资源
ms.assetid: b286b4b0-54f2-4798-a77b-c08743502552
keywords:
- 卸载例程 WDK 内核，非 PnP 驱动程序
- 非 PnP 卸载例程 WDK 内核
- 释放驱动程序分配的资源
- 驱动程序分配的资源版本 WDK 内核
- 资源释放 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41d352c7bf1cc49916b46617850c579ae27f9acf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185493"
---
# <a name="releasing-driver-allocated-resources"></a>释放驱动程序分配的资源





有关驱动程序如何使用注册表的详细信息，设置系统对象和其设备扩展中的资源、控制器扩展或驱动程序分配的非分页池因驱动程序而异。 但是，任何 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程都必须发布驱动程序在阶段中使用的资源。

任何驱动程序的 *Unload* 例程都必须确保当前没有其他驱动程序例程正在使用，或者可能很快会在释放该资源之前使用特定资源。

通常， *卸载* 例程会在以下阶段释放所有驱动程序分配的资源：

1.  如果驱动程序尚未执行此操作，请在任何物理设备上禁用中断（如果可能），然后在禁用中断后立即调用 [**IoDisconnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt) 。

2.  确保没有其他驱动程序例程可以引用 *卸载* 例程要释放的资源。

    例如，如果当前为特定设备对象启用了驱动程序的[*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程，则*卸载*例程必须调用[**IoStopTimer**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostoptimer) 。 它必须确保任何线程都不会等待任何驱动程序的调度程序对象，并且它的计时器对象在释放其调度程序对象的存储之前不会排队等待其 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 例程的调用。 如果它具有 ISR 可能已排队的[*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程，则必须调用[**KeRemoveQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovequeuedpc) ，依此类推。

    如果驱动程序调用 [**IoQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)，则它必须确保工作项已完成。 **IoQueueWorkItem** 接管关联设备对象上的引用;如果存在任何此类引用，则无法卸载该驱动程序。

    如果驱动程序调用 [**PsCreateSystemThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)，则 *卸载* 例程还必须导致运行驱动程序创建的线程，以便线程本身可以在卸载驱动程序之前调用 [**PsTerminateSystemThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-psterminatesystemthread) 。 驱动程序无法通过使用**PsCreateSystemThread**返回的*ThreadHandle*调用[**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)来释放驱动程序创建的系统线程。

3.  释放驱动程序分配的任何特定于设备的资源。 这样做可能需要调用以下系统支持例程：
    -   如果[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)或重新[*初始化*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)例程称为[**IoCreateSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)或[**IoCreateUnprotectedSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)，则为[**IoDeleteSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletesymboliclink) ; 如果驱动程序名为[**IoDeassignArcName**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioassignarcname)，则为[**IoAssignArcName**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeassignarcname) 。

    -   如果**DriverEntry**或任何其他名为[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)的驱动程序例程，并且驱动程序尚未释放已分配的内存，则为[**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 。

    -   如果**DriverEntry**或重新*初始化*例程称为[**MmMapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)，则为[**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) 。

    -   如果**DriverEntry**或重新*初始化*例程称为[**MmAllocateNonCachedMemory**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)，则为[**MmFreeNonCachedMemory**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmfreenoncachedmemory) 。

    -   如果**DriverEntry**或重新*初始化*例程称为[**MmAllocateContiguousMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)，则为[**MmFreeContiguousMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory) 。

    -   如果**DriverEntry**或重新*初始化*例程称为[**AllocateCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)，则为[**FreeCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_common_buffer) 。

    -   [**IoAssignResources**](./mmcreatemdl.md) 或 [**IoReportResourceUsage**](./mmcreatemdl.md) 如果 **DriverEntry** 或重新 *初始化* 例程称作其中一项支持例程或 [**HalAssignSlotResources**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) ，则会为自身和/或其物理设备单独声明配置注册表中的硬件资源。

4.  在设备对象的设备扩展中或在控制器对象的控制器扩展中设置 **DriverEntry** 或重新 *初始化* 例程的系统对象和资源（如果创建了一个) ） (。 具体而言，驱动程序必须先执行以下操作，然后才能尝试删除设备对象 ([**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)) 或控制器对象 ([**IoDeleteController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)) ：
    -   调用 [**IoDisconnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt) ，以释放存储在相应设备或控制器扩展中的中断对象指针。
    -   如果调用[**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)并将此指针存储在设备或控制器扩展中，请调用[**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) ，并将其指向下一个较低驱动程序的文件对象。
    -   如果调用[**IoAttachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)或[**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)并将此指针存储在设备或控制器扩展中，请调用[**IoDetachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice) ，并将其指向驱动程序的较低设备对象。

5.  在注册表中的** \\ 注册表 \\ 计算机 \\ 硬件 \\ Windows.applicationmodel.resources.core.resourcemap**树下，释放**DriverEntry**或重新*初始化*例程为驱动程序的物理设备（如果有）提供的硬件资源。

6.  删除其设备中存储在注册表下的**DriverEntry**或重新*初始化*例程的所有名称** \\ 。 \\DeviceMap**树。

驱动程序释放设备、系统和硬件资源后，可以删除其设备和控制器对象，如下一节中所述。

 

