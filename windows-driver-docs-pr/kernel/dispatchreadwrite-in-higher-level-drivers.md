---
title: 较高级驱动程序中的 DispatchReadWrite
description: 较高级驱动程序中的 DispatchReadWrite
ms.assetid: d8406115-c62e-4362-8d2c-77d0414c4104
keywords:
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE i/o 函数代码
- IRP_MJ_READ i/o 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读取/写入调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94aebb5d84ee5f59e184c4e8f8f7898029383586
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186725"
---
# <a name="dispatchreadwrite-in-higher-level-drivers"></a>较高级驱动程序中的 DispatchReadWrite





除了文件系统驱动程序，较高级别的驱动程序通常不会有任何用于 Irp 的内部驱动程序队列。 此类驱动程序的 [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程可以将具有有效参数的 irp 传递到更低版本的驱动程序，如设置其 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，如将 [Irp 向下传递到驱动程序堆栈](passing-irps-down-the-driver-stack.md)中所述。

但是，如果需要，SCSI 类驱动程序的 *DispatchReadWrite* 例程负责拆分大型传输请求，然后将 IRP 发送到主要的函数代码 [**irp \_ mj \_ READ**](./irp-mj-read.md) 或 [**IRP \_ mj \_ 写入**](./irp-mj-write.md) 到 SCSI 端口/微型端口驱动程序对。 有关详细信息，请参阅 [存储类驱动程序的 SplitTransferRequest 例程](../storage/storage-class-driver-s-splittransferrequest-routine.md)。

如果更高级别的驱动程序分配一个或多个 Irp，而该 Irp 在其 *DispatchReadWrite* 例程中为下一个较低的驱动程序设置，请求一些部分传输，则 *DispatchReadWrite* 例程必须与每个驱动程序分配的 IRP 一起调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 。 驱动程序必须注册其 *IoCompletion* 例程，以跟踪每个部分传输操作中传输的数据量，以便 *IoCompletion* 例程可以释放所有驱动程序分配的 irp，并最终完成原始请求。

如果底层驱动程序控制可移动媒体设备，则由较高级别的驱动程序分配的任何 Irp 都必须具有线程上下文。 若要设置线程上下文，分配的驱动程序必须设置 **Irp- &gt; Tail**。来自传入传输 IRP 中相同值的每个新分配的 IRP 中的线程。 有关详细信息，请参阅 [支持可移动介质](supporting-removable-media.md)。

如果基础设备驱动程序返回部分传输的 IRP，并出现错误， *IoCompletion* 例程可以重试部分传输请求，或使用返回的错误来完成原始 IRP，并在释放了更高级别的驱动程序分配的任何 irp 和内存后完成。

如果较高级别的驱动程序的 *DispatchReadWrite* 例程为部分传输操作分配内存，并且其分配将由驱动程序的 *IoCompletion* 例程 (或基础设备驱动程序) 访问，则 *DispatchReadWrite* 例程必须从非分页池分配该内存。

 

