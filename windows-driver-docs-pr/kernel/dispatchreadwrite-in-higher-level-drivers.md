---
title: 较高级驱动程序中的 DispatchReadWrite
description: 较高级驱动程序中的 DispatchReadWrite
ms.assetid: d8406115-c62e-4362-8d2c-77d0414c4104
keywords:
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE I/O 函数代码
- IRP_MJ_READ I/O 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读/写调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54b2b9918de2b89d0c6ed7d4777908a8402a6c72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384977"
---
# <a name="dispatchreadwrite-in-higher-level-drivers"></a>较高级驱动程序中的 DispatchReadWrite





除了文件系统驱动程序，更高级别的驱动程序通常不具有任何内部驱动程序队列的 Irp。 此类的驱动程序的[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以将 Irp 传递到较低的驱动程序的有效参数可能是设置后其[ *IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，如中所述[驱动程序堆栈的下层传递 Irp](passing-irps-down-the-driver-stack.md)。

但是，SCSI 类驱动程序的*DispatchReadWrite*例程负责拆分大型传输请求，如有必要，再发送与主要函数代码 IRP [ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write) SCSI 端口/微型端口驱动程序配对。 有关详细信息，请参阅[存储类驱动程序 SplitTransferRequest 例程](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-class-driver-s-splittransferrequest-routine)。

如果更高级别的驱动程序分配一个或多个 Irp，它为下一步低驱动程序中设置其*DispatchReadWrite*例程，以请求一定数量的部分传输*DispatchReadWrite*例程必须调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)与每个驱动程序分配的 IRP。 该驱动程序必须注册其*IoCompletion*例程，以跟踪每个部分传输操作中传输数据量，以便*IoCompletion*例程可发布所有驱动程序分配的 Irp 和最终，完成原始请求。

如果基础驱动程序控制可移动介质设备，由更高级别的驱动程序分配任何 Irp 必须具有线程上下文。 若要设置的线程上下文，但分配驱动程序必须设置**Irp-&gt;Tail.Overlay**。在每个线程新分配 IRP 中传入传输 IRP 的相同值。 有关详细信息，请参阅[支持可移动介质](supporting-removable-media.md)。

如果基础设备驱动程序返回一个错误，部分传输 IRP *IoCompletion*例程可以重试部分传输请求或完成其 I/O 状态块设置使用返回原始的 IRP错误，在释放任何 Irp 和内存的更高级别的驱动程序已分配。

如果更高级别的驱动程序的*DispatchReadWrite*例程的部分传输操作分配内存，并将由驱动程序的访问其分配*IoCompletion*例程 (或通过基础设备驱动程序）， *DispatchReadWrite*例程必须从非分页缓冲池分配的内存。

 

 




