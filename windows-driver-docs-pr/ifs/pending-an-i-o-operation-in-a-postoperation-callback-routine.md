---
title: 在后操作回调例程中挂起 I/O 操作
description: 在后操作回调例程中挂起 I/O 操作
ms.assetid: 126e13fb-51f6-4dcc-aa13-850921b3c752
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，挂起的操作
- 回调例程中挂起的 i/o 操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adafc1e13455253d82db9382f25c1d070ed7b3f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841039"
---
# <a name="pending-an-io-operation-in-a-postoperation-callback-routine"></a>在后操作回调例程中挂起 I/O 操作


## <span id="ddk_pending_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)可以通过执行以下步骤来挂起 i/o 操作：

1.  调用[**FltAllocateDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)为 i/o 操作分配工作项。

2.  调用[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)将 i/o 操作发送到系统工作队列。

3.  返回 FLT\_POSTOP\_需要\_更多\_处理。

请注意，如果下列任一条件成立，则对**FltQueueDeferredIoWorkItem**的调用将失败：

-   操作不是基于 IRP 的 i/o 操作。

-   此操作是一种分页 i/o 操作。

-   当前线程的**TopLevelIrp**字段不为**NULL**。 （有关如何查找此字段的值的详细信息，请参阅[**IoGetTopLevelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogettoplevelirp)。）

-   I/o 操作的目标实例被破坏。 （筛选器管理器通过将*标记*输入参数中的 FLTFL\_POST\_操作\_排出标志设置为 postoperation 回调例程来指示这种情况。）

必须准备好微筛选器驱动程序才能处理此故障。 如果你的微筛选器驱动程序无法处理此类故障，你应考虑使用[返回 FLT\_\_PREOP](returning-flt-preop-synchronize.md)中所述的方法，而不是挂起 i/o 操作。

在微筛选器驱动程序的 postoperation 回调例程返回 FLT\_POSTOP 后\_详细\_处理\_，筛选器管理器将不会为 i/o 操作执行任何进一步的完成处理，直至微微筛选器驱动程序的工作例程调用[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) ，以将操作控制返回到筛选器管理器。 此情况下，筛选器管理器不会执行任何进一步的处理，即使工作例程在操作的回调数据结构的**IoStatus**字段中设置了失败的 NTSTATUS 值也是如此。

取消排队和执行 i/o 操作的完成处理的工作例程必须调用**FltCompletePendedPostOperation** ，以将操作控制返回到筛选器管理器。

 

 




