---
title: 在后操作回调例程中挂起 I/O 操作
description: 在后操作回调例程中挂起 I/O 操作
ms.assetid: 126e13fb-51f6-4dcc-aa13-850921b3c752
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器中的挂起的操作
- 挂起的回调例程 WDK 中的 I/O 操作文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e050d4bbdebbbe7e357b7418114583eff5d6a62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386055"
---
# <a name="pending-an-io-operation-in-a-postoperation-callback-routine"></a>在后操作回调例程中挂起 I/O 操作


## <span id="ddk_pending_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)挂起 I/O 操作可以通过执行以下步骤：

1.  调用[ **FltAllocateDeferredIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)为 I/O 操作分配工作项。

2.  调用[ **FltQueueDeferredIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)发布到系统工作队列的 I/O 操作。

3.  返回 FLT\_POSTOP\_详细\_处理\_必需。

请注意，在调用**FltQueueDeferredIoWorkItem**如果任意下列条件为 true，则将失败：

-   该操作不是一个基于 IRP 的 I/O 操作。

-   操作已在分页 I/O 操作。

-   **TopLevelIrp**当前线程的字段不是**NULL**。 (有关如何查找此字段的值的详细信息，请参阅[ **IoGetTopLevelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogettoplevelirp)。)

-   正在销毁 I/O 操作的目标实例。 (筛选器管理器指示这种情况下，通过设置 FLTFL\_POST\_操作\_中的排出标志*标志*postoperation 回调例程的输入的参数。)

微筛选器驱动程序必须准备好处理此失败。 如果微筛选器驱动程序无法处理此类故障，则应考虑使用中所述的技术[返回 FLT\_PREOP\_同步](returning-flt-preop-synchronize.md)而不是挂起的 I/O 操作。

回调例程微筛选器驱动程序的 postoperation 后返回 FLT\_POSTOP\_详细\_处理\_必需的筛选器管理器将不执行任何进一步的完成处理的 I/O操作，直到微筛选器驱动程序的工作例程调用为止[ **FltCompletePendedPostOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)操作的控制权返回给筛选器管理器。 筛选器管理器将不执行任何进一步的处理这种情况即使工作例程设置失败 NTSTATUS 值**IoStatus.Status**操作的回调数据结构的字段。

取消排队并执行完成处理的 I/O 操作必须调用的工作例程**FltCompletePendedPostOperation**操作的控制权返回给筛选器管理器。

 

 




