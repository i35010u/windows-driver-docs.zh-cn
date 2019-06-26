---
title: 可选的 Dispatch 例程
description: 可选的 Dispatch 例程
ms.assetid: 38a3fcc9-237d-432d-85db-1594697c96a5
keywords:
- 调度例程 WDK 内核可选
- 可选的调度例程 WDK 内核
- 大容量存储设备 WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5061b7a9807d8c37da9a93cf507425a000a4ed36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384922"
---
# <a name="optional-dispatch-routines"></a>可选的 Dispatch 例程





驱动程序可能包括以下的调度例程：

-   [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_清理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)指示正在关闭与目标设备对象相关联的文件对象的最后一个句柄。 文件对象的未完成 I/O 请求可能仍存在。 驱动程序可以实现*DispatchCleanup*例程，以执行清理并不特定于任何特定的文件句柄。 驱动程序还可以使用其[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程实现相同目的。

-   [*DispatchQueryInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch), [*DispatchSetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    一些最高级别的驱动程序可能具有到进程[ **IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)并[ **IRP\_MJ\_设置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information) Irp。 此类请求指示用户模式应用程序、 内核模式组件或驱动程序已请求为用户模式下请求者具有句柄，或该文件对象 （表示驱动程序的设备对象） 的长度有关的信息将用户模式请求者正在尝试在该文件对象上设置文件结束。

    Parallel 类和串行设备驱动程序处理这些请求通过设置[**文件\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)或者[**文件\_位置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)长度或为零的位置。 其他最高级别的设备驱动程序应支持这些请求，尤其是在用户模式应用程序或内核模式驱动程序可能会调用 C 运行时函数来操作的文件对象。 文件系统驱动程序必须比这些最高级别的设备驱动程序的完全支持这些请求。

-   [*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    在设备缓存数据或在内部在驱动程序分配的内存中缓冲数据的驱动程序可能会收到[ **IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)。 此请求的回执指示驱动程序应将其缓冲的数据写入或刷新缓存的数据带到设备，或应放弃缓冲或缓存从设备读取的数据。

    例如，系统键盘和鼠标类驱动程序，它具有从他们的设备的输入数据的内部环缓冲区，支持刷新的请求。 大容量存储设备的驱动程序和它们的上面的驱动程序也支持此请求。

-   [*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    可能会在系统关闭之前，调用任何驱动程序必须处理[ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)。 *DispatchShutdown*例程应执行任何驱动程序确定清理之前有必要进行电源管理器将发送一个系统集 power IRP，若要关闭系统。 驱动程序可以调用[ **IoRegisterShutdownNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregistershutdownnotification)或[ **IoRegisterLastChanceShutdownNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)注册关闭通知。

大容量存储设备的驱动程序和它们的上层的中间驱动程序可以依赖最高级别的的文件系统驱动程序时在系统即将关闭的情况下发送关闭 Irp。 也就是说，FSD 是负责确保缓存的文件的任何数据写出到外围设备，调用基础驱动程序将从其设备缓存或缓冲区 （如果有） 和等的数据刷新之前系统关闭。

在内部缓存数据的大容量存储设备驱动程序必须提供*DispatchShutdown*并*DispatchFlushBuffers*例程。 如果大容量存储驱动程序在内存中缓冲数据，但其设备有无内部缓存，它还必须提供*DispatchShutdown*并*DispatchFlushBuffers*例程。

任何中间驱动程序上的驱动程序，处理分层[ **IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)并[ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)请求还提供了*DispatchShutdown*并*DispatchFlushBuffers*例程。

 

 




