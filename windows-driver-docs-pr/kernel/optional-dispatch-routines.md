---
title: 可选的 Dispatch 例程
description: 可选的 Dispatch 例程
ms.assetid: 38a3fcc9-237d-432d-85db-1594697c96a5
keywords:
- 调度例程 WDK 内核，可选
- 可选调度例程 WDK 内核
- 大容量存储设备 WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91eab670c8d73244748bd778682aa5ce5daeb065
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827722"
---
# <a name="optional-dispatch-routines"></a>可选的 Dispatch 例程





驱动程序可能包含以下调度例程：

-   [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_清除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)指示正在关闭与目标设备对象相关联的文件对象的最后一个句柄。 文件对象的未完成 i/o 请求可能仍然存在。 驱动程序可以实现*DispatchCleanup*例程，以执行不特定于任何特定文件句柄的清理。 驱动程序还可以将其[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程用于相同的目的。

-   [*DispatchQueryInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [ *DispatchSetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    某些高级驱动程序可能必须处理[**IRP\_mj\_QUERY\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)和[**IRP\_MJ\_集\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)irp。 此类请求指示用户模式应用程序、内核模式组件或驱动程序已请求有关用户模式请求程序具有其句柄的文件对象的长度的信息，或者为用户模式请求者正在尝试对该文件对象设置文件尾。

    并行类和串行设备驱动程序通过将[**文件\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)或[**文件\_位置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)长度或位置设置为零来处理这些请求。 其他最高级别的设备驱动程序应该支持这些请求，尤其是在用户模式应用程序或内核模式驱动程序可能调用 C 运行时函数来操作文件对象时。 文件系统驱动程序必须比这些最高级别的设备驱动程序更完全支持这些请求。

-   [*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    缓存设备中的数据或在驱动程序分配的内存内部缓冲数据的驱动程序可能会接收[**IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)。 此请求的接收表明驱动程序应该写入其缓冲数据，或将缓存的数据刷新到设备，或者应丢弃从设备读取的缓冲数据或缓存数据。

    例如，系统键盘和鼠标类驱动程序（在其设备中提供输入数据的内部环形缓冲区）支持刷新请求。 大容量存储设备和其上方分层驱动程序的驱动程序也支持此请求。

-   [*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    任何可能在系统关闭之前调用的驱动程序都必须处理[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)。 在电源管理器发送系统设置-power IRP 关闭系统之前， *DispatchShutdown*例程应执行任何驱动程序确定的清理。 驱动程序可以调用[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)或[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)来注册关闭通知。

大容量存储设备的驱动程序和在其上分层的中间驱动程序可以依赖于一个最高级别的文件系统驱动程序，以便在系统即将关闭时向其发送关闭 Irp。 也就是说，FSD 负责确保将所有缓存的文件数据写出到外围设备，调用底层驱动程序以刷新其设备缓存或缓冲区中的数据（如果有），然后再关闭系统。

内部缓存数据的大容量存储设备的驱动程序必须提供*DispatchShutdown*和*DispatchFlushBuffers*例程。 如果大容量存储驱动程序在内存中缓冲数据，但其设备没有内部缓存，还必须提供*DispatchShutdown*和*DispatchFlushBuffers*例程。

任何位于驱动程序之上的中间驱动程序，用于处理[**IRP\_mj\_FLUSH\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)和[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)请求还提供了*DispatchShutdown*和*DispatchFlushBuffers*例程.

 

 




