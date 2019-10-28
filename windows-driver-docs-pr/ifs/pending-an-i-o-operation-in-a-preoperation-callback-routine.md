---
title: 在预操作回调例程中挂起 I/O 操作
description: 在预操作回调例程中挂起 I/O 操作
ms.assetid: 39b04911-c0d9-42ec-b93e-b440b12f9e41
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，挂起的操作
- 回调例程中挂起的 i/o 操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba29a922377502458583a7227a93103fa5a0331
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841037"
---
# <a name="pending-an-io-operation-in-a-preoperation-callback-routine"></a>在预操作回调例程中挂起 I/O 操作


## <span id="ddk_pending_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)可以通过将操作发布到系统工作队列并返回 FLT\_PREOP\_挂起来挂起 i/o 操作。 返回此状态值表明微筛选器驱动程序将控制 i/o 操作，直到调用[**FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)恢复处理 i/o 操作。

通过执行以下步骤，微筛选器驱动程序的 preoperation 回调例程 pends i/o 操作：

1.  通过调用例程（如[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)）将 i/o 操作发布到系统工作队列。

2.  返回 FLT\_PREOP\_挂起。

必须挂起所有（或大部分）传入 i/o 操作的微筛选器驱动程序不应使用诸如**FltQueueDeferredIoWorkItem**这样的例程来挂起操作，因为调用此例程会导致系统工作队列溢出。 相反，此类微筛选器驱动程序应使用取消安全队列。 有关使用取消安全队列的详细信息，请参阅[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)。

请注意，如果下列任一条件成立，则对**FltQueueDeferredIoWorkItem**的调用将失败：

-   操作不是基于 IRP 的 i/o 操作。

-   此操作是一种分页 i/o 操作。

-   当前线程的**TopLevelIrp**字段不为**NULL**。 （有关如何查找此字段的值的详细信息，请参阅[**IoGetTopLevelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogettoplevelirp)。）

-   I/o 操作的目标实例被破坏。

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT\_PREOP\_挂起，则它必须在*CompletionContext* output 参数中返回**NULL** 。

微筛选器驱动程序只能为基于 IRP 的 i/o 操作返回 FLT\_PREOP\_挂起。 若要确定某个操作是否是基于 IRP 的 i/o 操作，请使用[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))宏。

取消排队和处理 i/o 操作的工作例程必须调用**FltCompletePendedPreOperation**才能恢复操作的处理。

 

 




