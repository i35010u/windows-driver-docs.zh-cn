---
title: 在后操作回调例程中挂起 I/O 操作
description: 在后操作回调例程中挂起 I/O 操作
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，挂起的操作
- 回调例程中挂起的 i/o 操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ec31bafa39b1cd7d33df15feb0d5117a6dc4ab5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816251"
---
# <a name="pending-an-io-operation-in-a-postoperation-callback-routine"></a>在后操作回调例程中挂起 I/O 操作


## <span id="ddk_pending_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 可以通过执行以下步骤来挂起 i/o 操作：

1.  调用 [**FltAllocateDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem) 为 i/o 操作分配工作项。

2.  调用 [**FltQueueDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem) 将 i/o 操作发送到系统工作队列。

3.  返回 FLT \_ POSTOP \_ 需要更多 \_ \_ 的处理。

请注意，如果下列任一条件成立，则对 **FltQueueDeferredIoWorkItem** 的调用将失败：

-   操作不是基于 IRP 的 i/o 操作。

-   此操作是一种分页 i/o 操作。

-   当前线程的 **TopLevelIrp** 字段不为 **NULL**。  (有关如何查找此字段的值的详细信息，请参阅 [**IoGetTopLevelIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogettoplevelirp)。 ) 

-   I/o 操作的目标实例被破坏。  (筛选器管理器通过将 \_ \_ \_ *标志* 输入参数中的 FLTFL POST 操作排出标志设置为 postoperation 回调例程来指示这种情况。 ) 

必须准备好微筛选器驱动程序才能处理此故障。 如果你的微筛选器驱动程序无法处理此类故障，你应考虑使用 [返回 FLT \_ PREOP \_ 同步](returning-flt-preop-synchronize.md) 而不是挂起 i/o 操作中所述的方法。

在微筛选器驱动程序的 postoperation 回调例程返回 FLT \_ POSTOP \_ 需要更多 \_ 处理后 \_ ，筛选器管理器将不会为 i/o 操作执行任何进一步的完成处理，直到微筛选器驱动程序的工作例程调用 [**FltCompletePendedPostOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) ，才能将操作控制返回到筛选器管理器。 此情况下，筛选器管理器不会执行任何进一步的处理，即使工作例程在操作的回调数据结构的 **IoStatus** 字段中设置了失败的 NTSTATUS 值也是如此。

取消排队和执行 i/o 操作的完成处理的工作例程必须调用 **FltCompletePendedPostOperation** ，以将操作控制返回到筛选器管理器。

 

