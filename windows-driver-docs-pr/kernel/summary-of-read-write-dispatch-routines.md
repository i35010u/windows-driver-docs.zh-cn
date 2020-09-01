---
title: 读/写 Dispatch 例程摘要
description: 读/写 Dispatch 例程摘要
ms.assetid: 2ab1cde7-89e8-449f-b2a0-12aa0762ebf3
keywords:
- DispatchRead 例程
- DispatchWrite 例程
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchWrite 例程
- 调度例程 WDK 内核，DispatchRead 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE i/o 函数代码
- IRP_MJ_READ i/o 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读取/写入调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f506b55c688ce09f0a084c508ce8329080a633
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186183"
---
# <a name="summary-of-readwrite-dispatch-routines"></a>读/写 Dispatch 例程摘要





实现 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)或 [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程时，请记住以下几点：

-   分层驱动程序链中的最高级别的驱动程序负责检查传入的读/写 Irp 的参数是否有效，然后再在 IRP 中设置下一个较低级别的驱动程序的 i/o 堆栈位置。

-   中间和最低级别驱动程序通常可以依赖于其链中的最高级别的驱动程序来向下传递包含有效参数的传输请求。 但是，任何驱动程序都可以对 IRP 的 i/o 堆栈位置中的参数执行健全性检查，并且每个设备驱动程序都应检查参数中是否存在可能违反其设备施加的任何限制的情况。

-   如果*DispatchReadWrite*例程完成了一个具有错误的 IRP，则它应使用适当的 NTSTATUS 类型值设置 i/o 堆栈位置**状态**成员，将**信息**成员设置为零，并使用 IRP 和 IO 的*PriorityBoost*调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，而 \_ 不是 \_ 增量。

-   如果驱动程序使用缓冲 i/o，则可能需要定义一个结构，使其包含要传输的数据，并且可能需要在内部缓冲一些这类结构。

-   如果驱动程序使用直接 i/o，则可能需要检查 **Irp &gt; MdlAddress** 中的 MDL 是否描述了包含过多数据 (的缓冲区，或在单个传输操作中处理基础设备的过多分页符) 。 如果是这样，则驱动程序必须将原始传输请求拆分为较小的传输操作序列。

    紧耦合的类驱动程序可以将此类请求拆分为其基本端口驱动程序的 *DispatchReadWrite* 例程。 要执行此操作，需要 SCSI 类驱动程序，特别是大容量存储设备。 有关 SCSI 驱动程序要求的详细信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

-   较低级别的设备驱动程序的 *DispatchReadWrite* 例程应延迟将大型传输请求拆分为部分传输，直到另一个驱动程序例程取消排队 IRP 来设置用于传输的设备。

-   如果较低级别的设备驱动程序将读取/写入 IRP 排队以供其自己的例程进一步处理，则必须在将 IRP 排队之前调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 。 在这些情况下， *DispatchReadWrite* 例程还必须返回状态为 "挂起" 的控制 \_ 。

-   如果 *DispatchReadWrite* 例程将 irp 传递到较低的驱动程序，则必须在 irp 中设置下一个较低驱动程序的 i/o 堆栈位置。 更高级别的驱动程序是否还会在将其传递到[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之前在 IRP 中设置[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，这取决于驱动程序的设计及其下分层的。

    但是，更高级别的驱动程序必须先调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，然后才能调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （如果它分配了 irp 或内存等资源）。 如果较低的驱动程序完成了请求，但在*IoCompletion*例程调用[**IOCOMPLETEREQUEST**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)与原始 IRP 之前，则其*IoCompletion*例程必须释放任何驱动程序分配的资源。

-   如果较高级别的驱动程序为可能包含基础可移动媒体设备驱动程序的较低驱动程序分配 Irp，则分配的驱动程序必须在它分配的每个 IRP 中建立线程上下文。

 

