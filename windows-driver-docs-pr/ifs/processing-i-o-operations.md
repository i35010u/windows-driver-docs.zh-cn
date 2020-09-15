---
title: 处理 I/O 操作
description: 处理 I/O 操作
ms.assetid: 750fa89b-dbdf-45ff-bfa5-83c717d2d7bb
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，处理 i/o 操作
- preoperation 回调例程 WDK 文件系统微筛选器，筛选器管理器
- postoperation 回调例程 WDK 文件系统微筛选器，筛选器管理器
- 机会锁定 WDK 文件系统微筛选器
- 锁定 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17f12678e106f006c8ccb465051f17663377ff0e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104512"
---
# <a name="processing-io-operations"></a>处理 I/O 操作


筛选器管理器简化了微筛选器驱动程序的 i/o 操作处理。 与旧版筛选器驱动程序不同，必须将所有 i/o 请求正确地传递到下一个较低版本的驱动程序，并正确处理挂起的请求、同步和 i/o 完成，无论旧筛选器驱动程序是否执行与请求相关的任何工作，一个微筛选器驱动程序都只注册它必须处理的 i/o 操作。

对于给定 i/o 操作，筛选器管理器仅调用已为该操作注册了 [**preoperation 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 例程的微筛选器驱动程序。 筛选器管理器还代表微筛选器驱动程序处理某些 IRP 维护任务，例如将参数复制到下一个堆栈位置并传播 IRP **PendingReturned** 标志。

在其 preoperation 回调例程中，微筛选器驱动程序将执行 i/o 操作所需的任何处理，并通过从其 preoperation 回调例程返回相应的值来指示对 IRP 应执行的操作。 例如，若要在没有完成例程的情况下将 IRP 转发到下一个较低版本的驱动程序，微筛选器驱动程序将返回 FLT \_ PREOP \_ SUCCESS \_ NO \_ 回拨; 若要执行与完成例程相同的操作， (微筛选器驱动程序的 postoperation 回调例程来实现 i/o 操作) ，则微筛选器驱动程序将返回 FLT \_ PREOP \_ SUCCESS \_ \_ 。

如果需要，可以通过调用 [**FltQueueDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)将操作通过其 preoperation 回调例程排队给工作线程。 完成此操作后，微筛选器驱动程序将 \_ \_ 从其 preoperation 回调例程返回 FLT PREOP，以指示 i/o 操作处于挂起状态，而微筛选器驱动程序负责完成或恢复处理请求。 若要继续处理，微筛选器驱动程序将从工作线程调用 [**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation) 。

如果微筛选器驱动程序需要维护其自己的按实例取消安全队列来处理未完成的 i/o 操作，则可以设置此类队列，方法是：在其*InstanceSetupCallback*例程中调用[*FltCbdqInitialize*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize) ，并根据需要在其 preoperation 回调例程中调用[*FltCbdqInsertIo*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinsertio) ，将 i/o 操作插入队列。

如果 (旧筛选器和微筛选器驱动程序) 完成处理后，筛选器管理器会为 i/o 操作调用微筛选器驱动程序的 [**postoperation 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 例程。

微筛选器驱动程序可在其 postoperation 回调例程中调用 [**FltDoCompletionProcessingWhenSafe**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe) ，以确保在安全的 IRQL 处执行完成处理。 如果需要，还可以通过调用 [**FltQueueDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)将操作的完成处理排队到工作线程。 完成此操作后，微筛选器驱动程序将 \_ \_ \_ 从其 postoperation 回调例程返回 FLT POSTOP 更多的处理， \_ 以暂停筛选器管理器对 i/o 操作的完成处理。 若要继续完成处理，微筛选器驱动程序将从工作线程调用 [**FltCompletePendedPostOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) 。

筛选器管理器支持对 "通用" 工作项进行排队-与微筛选器驱动程序或微筛选器驱动程序实例相关联的工作项，而不是 i/o 操作。 微筛选器驱动程序可以通过调用 [**FltQueueGenericWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)将工作项插入到系统工作队列中。 此例程类似于 [**ExQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exqueueworkitem)等例程;例如，工作项 (通过调用 [**FltAllocateGenericWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)) 分配，可以重复使用。 不过， **FltQueueGenericWorkItem** 更安全，因为筛选器驱动程序不能在处理未完成的工作项时进行卸载，所以筛选器驱动程序不允许卸载微筛选器驱动程序或筛选器驱动程序实例。

筛选器管理器还提供对机会锁定 (oplock) 操作的支持。 对于 oplock 操作，微筛选器驱动程序可以将此类筛选器例程用作 [**FltInitializeOplock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock) 和 [**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)，它们等效于文件系统和旧筛选器驱动程序使用的 **FsRtlInitializeOplock** 和 **FsRtlOplockFsctrl** 例程。

### <a name="span-idfilter_manager_routines_for_processing_i_o_operationsspanspan-idfilter_manager_routines_for_processing_i_o_operationsspanspan-idfilter_manager_routines_for_processing_i_o_operationsspanfilter-manager-routines-for-processing-io-operations"></a><span id="Filter_Manager_Routines_for_Processing_I_O_Operations"></span><span id="filter_manager_routines_for_processing_i_o_operations"></span><span id="FILTER_MANAGER_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>用于处理 i/o 操作的筛选器管理器例程

筛选器管理器为 [**preoperation**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 和 [**postoperation**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 回调例程中的挂起 i/o 提供以下支持例程：

[**FltCompletePendedPostOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)

[**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)

[**FltDoCompletionProcessingWhenSafe**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)

以下例程用于在 preoperation 和 postoperation 回调例程中对工作项进行排队：

[**FltAllocateDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)

[**FltAllocateGenericWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)

[**FltFreeDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreedeferredioworkitem)

[**FltFreeGenericWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreegenericworkitem)

[**FltQueueDeferredIoWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)

[**FltQueueGenericWorkItem**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)

以下例程提供取消安全队列支持：

[*FltCbdqDisable*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqdisable)

[*FltCbdqEnable*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqenable)

[*FltCbdqInitialize*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)

[*FltCbdqInsertIo*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinsertio)

[*FltCbdqRemoveIo*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqremoveio)

[*FltCbdqRemoveNextIo*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqremovenextio)

以下例程提供 oplock 支持：

[*FltCheckOplock*](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcheckoplock)

[**FltCurrentBatchOplock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcurrentbatchoplock)

[**FltInitializeOplock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock)

[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FltOplockIsFastIoPossible**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockisfastiopossible)

[**FltUninitializeOplock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializeoplock)

### <a name="span-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanspan-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanspan-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanminifilter-driver-callback-routines-for-processing-io-operations"></a><span id="Minifilter_Driver_Callback_Routines_for_Processing_I_O_Operations"></span><span id="minifilter_driver_callback_routines_for_processing_i_o_operations"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>用于处理 i/o 操作的微筛选器驱动程序回调例程

对于微筛选器驱动程序处理的每个 i/o 操作类型，以下回调例程均存储在 [**FLT \_ 操作 \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration) 结构中：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调例程名称</th>
<th align="left">回调例程类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>PostOperation</em></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_POST_OPERATION_CALLBACK&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)"><strong>PFLT_POST_OPERATION_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>PreOperation</em></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

