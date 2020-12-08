---
title: 在预操作回调例程中挂起 I/O 操作
description: 在预操作回调例程中挂起 I/O 操作
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，挂起的操作
- 回调例程中挂起的 i/o 操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d595e8c6ddfcac8139338a97e2e71fe4fd45ed83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816253"
---
# <a name="pending-an-io-operation-in-a-preoperation-callback-routine"></a>在预操作回调例程中挂起 I/O 操作


## <span id="ddk_pending_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 可以通过将操作发布到系统工作队列并返回 FLT PREOP 待定操作来挂起 i/o 操作 \_ \_ 。 返回此状态值表明微筛选器驱动程序将控制 i/o 操作，直到调用 [**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation) 恢复处理 i/o 操作。

通过执行以下步骤，微筛选器驱动程序的 preoperation 回调例程 pends i/o 操作：

1.  通过调用例程（如 [**FltQueueDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)）将 i/o 操作发布到系统工作队列。

2.  返回 FLT \_ PREOP \_ PENDING。

必须挂起所有 (或大多数) 传入 i/o 操作的微筛选器驱动程序不应使用诸如 **FltQueueDeferredIoWorkItem** 这样的例程来挂起操作，因为调用此例程会导致系统工作队列溢出。 相反，此类微筛选器驱动程序应使用取消安全队列。 有关使用取消安全队列的详细信息，请参阅 [*FltCbdqInitialize*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)。

请注意，如果下列任一条件成立，则对 **FltQueueDeferredIoWorkItem** 的调用将失败：

-   操作不是基于 IRP 的 i/o 操作。

-   此操作是一种分页 i/o 操作。

-   当前线程的 **TopLevelIrp** 字段不为 **NULL**。  (有关如何查找此字段的值的详细信息，请参阅 [**IoGetTopLevelIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogettoplevelirp)。 ) 

-   I/o 操作的目标实例被破坏。

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT \_ PREOP \_ PENDING，则它必须在 *CompletionContext* Output 参数中返回 **NULL** 。

微筛选器驱动程序只能 \_ \_ 为基于 IRP 的 i/o 操作返回 FLT PREOP PENDING。 若要确定某个操作是否为基于 IRP 的 i/o 操作，请使用 [**FLT \_ 为 \_ irp \_ 操作**](/previous-versions/ff544654(v=vs.85)) 宏。

取消排队和处理 i/o 操作的工作例程必须调用 **FltCompletePendedPreOperation** 才能恢复操作的处理。

 

