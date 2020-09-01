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
ms.openlocfilehash: 372570d1bfa6efb9ba690b0be125a1bb761a0313
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191855"
---
# <a name="optional-dispatch-routines"></a>可选的 Dispatch 例程





驱动程序可能包含以下调度例程：

-   [*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_"MJ \_ 清除**](./irp-mj-cleanup.md) " 指示正在关闭与目标设备对象相关联的文件对象的最后一个句柄。 文件对象的未完成 i/o 请求可能仍然存在。 驱动程序可以实现 *DispatchCleanup* 例程，以执行不特定于任何特定文件句柄的清理。 驱动程序还可以将其 [*DispatchClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程用于相同的目的。

-   [*DispatchQueryInformation*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [ *DispatchSetInformation*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    某些高级驱动程序可能必须处理 [**irp \_ mj \_ 查询 \_ 信息**](./irp-mj-query-information.md) 和 [**irp \_ mj \_ 集 \_ 信息**](./irp-mj-set-information.md) irp。 此类请求表明，用户模式应用程序、内核模式组件或驱动程序请求了有关 file 对象长度的信息， (表示驱动程序的设备对象) 用户模式请求程序具有其句柄，或者用户模式请求方正在尝试设置该文件对象的文件尾。

    并行类和串行设备驱动程序通过将 [**文件 \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information) 或 [**文件 \_ 位置 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information) 长度或位置设置为零来处理这些请求。 其他最高级别的设备驱动程序应该支持这些请求，尤其是在用户模式应用程序或内核模式驱动程序可能调用 C 运行时函数来操作文件对象时。 文件系统驱动程序必须比这些最高级别的设备驱动程序更完全支持这些请求。

-   [*DispatchFlushBuffers*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    缓存设备中的数据或在由驱动程序分配的内存内部缓冲数据的驱动程序可能会收到 [**IRP \_ MJ \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md)。 此请求的接收表明驱动程序应该写入其缓冲数据，或将缓存的数据刷新到设备，或者应丢弃从设备读取的缓冲数据或缓存数据。

    例如，系统键盘和鼠标类驱动程序（在其设备中提供输入数据的内部环形缓冲区）支持刷新请求。 大容量存储设备和其上方分层驱动程序的驱动程序也支持此请求。

-   [*DispatchShutdown*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    任何可能在系统关闭之前调用的驱动程序必须处理 [**IRP \_ MJ \_ 关闭**](./irp-mj-shutdown.md)。 在电源管理器发送系统设置-power IRP 关闭系统之前， *DispatchShutdown* 例程应执行任何驱动程序确定的清理。 驱动程序可以调用 [**IoRegisterShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification) 或 [**IoRegisterLastChanceShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification) 来注册关闭通知。

大容量存储设备的驱动程序和在其上分层的中间驱动程序可以依赖于一个最高级别的文件系统驱动程序，以便在系统即将关闭时向其发送关闭 Irp。 也就是说，FSD 负责确保将任何缓存的文件数据写出到外围设备，并调用基础驱动程序以刷新其设备缓存或缓冲区中的数据， (如果任何) ，则在系统关闭之前。

内部缓存数据的大容量存储设备的驱动程序必须提供 *DispatchShutdown* 和 *DispatchFlushBuffers* 例程。 如果大容量存储驱动程序在内存中缓冲数据，但其设备没有内部缓存，还必须提供 *DispatchShutdown* 和 *DispatchFlushBuffers* 例程。

在处理 [**IRP \_ mj \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md) 和 [**IRP \_ mj \_ 关闭**](./irp-mj-shutdown.md) 请求的驱动程序上分层的任何中间驱动程序也提供了 *DispatchShutdown* 和 *DispatchFlushBuffers* 例程。

 

