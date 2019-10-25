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
ms.openlocfilehash: ddfd2831410c51da04126f6b91fbd050367ade98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836840"
---
# <a name="dispatchreadwrite-in-higher-level-drivers"></a>较高级驱动程序中的 DispatchReadWrite





除了文件系统驱动程序，较高级别的驱动程序通常不会有任何用于 Irp 的内部驱动程序队列。 此类驱动程序的[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程可以将具有有效参数的 irp 传递到更低版本的驱动程序，如设置其[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，如将[Irp 向下传递到驱动程序堆栈](passing-irps-down-the-driver-stack.md)中所述。

但是，如果需要，SCSI 类驱动程序的*DispatchReadWrite*例程负责拆分大型传输请求，然后将 IRP 发送到主要函数代码[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)或[**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)SCSI 端口/微型端口驱动程序对。 有关详细信息，请参阅[存储类驱动程序的 SplitTransferRequest 例程](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-class-driver-s-splittransferrequest-routine)。

如果更高级别的驱动程序分配一个或多个 Irp，而该 Irp 在其*DispatchReadWrite*例程中为下一个较低版本的驱动程序进行了设置，则若要请求某些部分传输， *DispatchReadWrite*例程必须调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)每个驱动程序分配的 IRP。 驱动程序必须注册其*IoCompletion*例程，以跟踪在每个部分传输操作中传输的数据量，以便*IoCompletion*例程可以释放所有驱动程序分配的 irp，并最终完成原始请求.

如果底层驱动程序控制可移动媒体设备，则由较高级别的驱动程序分配的任何 Irp 都必须具有线程上下文。 若要设置线程上下文，分配的驱动程序必须将**Irp&gt;** 。来自传入传输 IRP 中相同值的每个新分配的 IRP 中的线程。 有关详细信息，请参阅[支持可移动介质](supporting-removable-media.md)。

如果基础设备驱动程序返回一个用于部分传输的 IRP，并出现错误， *IoCompletion*例程可以重试部分传输请求，或使用返回的错误来完成原始 IRP，并在释放任何已分配更高级别驱动程序的 Irp 和内存。

如果较高级别的驱动程序的*DispatchReadWrite*例程为部分传输操作分配内存，并且驱动程序的*IoCompletion*例程（或基础设备驱动程序）将访问其分配， *DispatchReadWrite*例程必须从非分页池分配该内存。

 

 




