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
ms.openlocfilehash: f27eddc036058e17a182f565ecb90f1495ab9e10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841023"
---
# <a name="processing-io-operations"></a>处理 I/O 操作


筛选器管理器简化了微筛选器驱动程序的 i/o 操作处理。 与旧版筛选器驱动程序不同，该驱动程序必须将所有 i/o 请求正确地传递到下一个较低版本的驱动程序，并正确处理挂起的请求、同步和 i/o 完成，而无论旧筛选器驱动程序是否执行与请求相关的任何工作（微筛选器驱动程序）仅注册它必须处理的 i/o 操作。

对于给定 i/o 操作，筛选器管理器仅调用已为该操作注册了[**preoperation 回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)例程的微筛选器驱动程序。 筛选器管理器还代表微筛选器驱动程序处理某些 IRP 维护任务，例如将参数复制到下一个堆栈位置并传播 IRP **PendingReturned**标志。

在其 preoperation 回调例程中，微筛选器驱动程序将执行 i/o 操作所需的任何处理，并通过从其 preoperation 回调例程返回相应的值来指示对 IRP 应执行的操作。 例如，若要将 IRP 转发到不带完成例程的下一个较低版本的驱动程序，微筛选器驱动程序将返回 FLT\_PREOP\_SUCCESS\_不\_回拨;若要使用完成例程（微筛选器驱动程序的 postoperation 回调例程进行 i/o 操作）执行相同操作，微筛选器驱动程序将返回 FLT\_PREOP\_SUCCESS\_\_回拨。

如果需要，可以通过调用[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)将操作通过其 preoperation 回调例程排队给工作线程。 完成此操作后，微筛选器驱动程序将从其 preoperation 回调例程返回 FLT\_PREOP\_，以指示 i/o 操作处于挂起状态，并且微筛选器驱动程序负责完成或恢复处理请求. 若要继续处理，微筛选器驱动程序将从工作线程调用[**FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation) 。

如果微筛选器驱动程序需要维护其自己的按实例取消安全队列来处理未完成的 i/o 操作，则可以通过在其 InstanceSetupCallback 例程中调用[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)来设置此类队列，并调用[*FltCbdqInsertIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinsertio)在其 preoperation 回调例程中插入 i/o 操作到队列中。

筛选器驱动程序（旧筛选器和微筛选器驱动程序）完成处理后，筛选器管理器会为 i/o 操作调用微筛选器驱动程序的[**postoperation 回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)例程。

微筛选器驱动程序可在其 postoperation 回调例程中调用[**FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe) ，以确保在安全的 IRQL 处执行完成处理。 如果需要，还可以通过调用[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)将操作的完成处理排队到工作线程。 完成此操作后，微筛选器驱动程序将返回 FLT\_POSTOP\_从其 postoperation 回调例程中获取更多\_处理\_，以暂停筛选器管理器对 i/o 操作的完成处理。 若要继续完成处理，微筛选器驱动程序将从工作线程调用[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) 。

筛选器管理器支持对 "通用" 工作项进行排队-与微筛选器驱动程序或微筛选器驱动程序实例相关联的工作项，而不是 i/o 操作。 微筛选器驱动程序可以通过调用[**FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)将工作项插入到系统工作队列中。 此例程类似于[**ExQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exqueueworkitem)等例程;例如，可以重复使用工作项（通过调用[**FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)分配）。 不过， **FltQueueGenericWorkItem**更安全，因为筛选器驱动程序不能在处理未完成的工作项时进行卸载，所以筛选器驱动程序不允许卸载微筛选器驱动程序或筛选器驱动程序实例。

筛选器管理器还提供对机会锁定（oplock）操作的支持。 对于 oplock 操作，微筛选器驱动程序可以将此类筛选器例程用作[**FltInitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock)和[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)，它们等效于由文件系统和旧筛选器驱动程序使用。

### <a name="span-idfilter_manager_routines_for_processing_i_o_operationsspanspan-idfilter_manager_routines_for_processing_i_o_operationsspanspan-idfilter_manager_routines_for_processing_i_o_operationsspanfilter-manager-routines-for-processing-io-operations"></a><span id="Filter_Manager_Routines_for_Processing_I_O_Operations"></span><span id="filter_manager_routines_for_processing_i_o_operations"></span><span id="FILTER_MANAGER_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>用于处理 i/o 操作的筛选器管理器例程

筛选器管理器为[**preoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)和[**postoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)回调例程中的挂起 i/o 提供以下支持例程：

[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)

[**FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)

[**FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)

以下例程用于在 preoperation 和 postoperation 回调例程中对工作项进行排队：

[**FltAllocateDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)

[**FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)

[**FltFreeDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreedeferredioworkitem)

[**FltFreeGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreegenericworkitem)

[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)

[**FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)

以下例程提供取消安全队列支持：

[*FltCbdqDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqdisable)

[*FltCbdqEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqenable)

[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)

[*FltCbdqInsertIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinsertio)

[*FltCbdqRemoveIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqremoveio)

[*FltCbdqRemoveNextIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqremovenextio)

以下例程提供 oplock 支持：

[*FltCheckOplock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcheckoplock)

[**FltCurrentBatchOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcurrentbatchoplock)

[**FltInitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FltOplockIsFastIoPossible**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockisfastiopossible)

[**FltUninitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializeoplock)

### <a name="span-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanspan-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanspan-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanminifilter-driver-callback-routines-for-processing-io-operations"></a><span id="Minifilter_Driver_Callback_Routines_for_Processing_I_O_Operations"></span><span id="minifilter_driver_callback_routines_for_processing_i_o_operations"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>用于处理 i/o 操作的微筛选器驱动程序回调例程

以下回调例程存储在微筛选器驱动程序处理的每种 i/o 操作类型的[**FLT\_操作\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration)结构中：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_POST_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)"><strong>PFLT_POST_OPERATION_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>PreOperation</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




