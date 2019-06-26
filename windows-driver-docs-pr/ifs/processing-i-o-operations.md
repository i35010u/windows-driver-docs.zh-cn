---
title: 处理 I/O 操作
description: 处理 I/O 操作
ms.assetid: 750fa89b-dbdf-45ff-bfa5-83c717d2d7bb
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，处理 I/O 操作
- preoperation 回调例程 WDK 文件系统微筛选器，筛选器管理器
- postoperation 回调例程 WDK 文件系统微筛选器，筛选器管理器
- 伺机锁定 WDK 文件系统微筛选器
- 锁定 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32f0f06ba6b20947f252557d2d0c526999755055
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385153"
---
# <a name="processing-io-operations"></a>处理 I/O 操作


筛选器管理器可简化微筛选器驱动程序处理 I/O 操作。 与传统的筛选器驱动程序，它必须正确地将所有 I/O 请求都传递到下一个较低的驱动程序和旧的筛选器驱动程序执行任何工作是否正确处理挂起的请求、 同步和 I/O 完成与请求相关，微筛选器驱动程序仅对必须处理的 I/O 操作的寄存器。

对于给定的 I/O 操作，筛选器管理器调用仅微筛选器驱动程序的已注册[ **preoperation 回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)例行为该操作。 筛选器管理器还可以处理某些 IRP 维护任务代表微筛选器驱动程序，如将参数复制到下一步的堆栈位置和传播 IRP **PendingReturned**标志。

在其 preoperation 回调例程中，微筛选器驱动程序执行任何处理所需的 I/O 操作和指示该怎么办呢 IRP 到通过从其 preoperation 回调例程返回适当的值。 例如，要将转发到下一步低驱动程序而无需完成例程 IRP，微筛选器驱动程序返回 FLT\_PREOP\_成功\_否\_回调; 若要执行完成例程 (使用相同的操作微筛选器驱动程序的 postoperation 回调例程的 I/O 操作），微筛选器驱动程序将返回 FLT\_PREOP\_成功\_WITH\_回调。

在其 preoperation 回调例程中，微筛选器驱动程序可以排入队列工作线程上的操作根据需要通过调用[ **FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)。 这样做之后，微筛选器驱动程序返回 FLT\_PREOP\_PENDING 从其 preoperation 回调例程，以指示 I/O 操作处于挂起状态，并且微筛选器驱动程序负责完成或恢复的处理该请求。 若要继续处理微筛选器驱动程序调用[ **FltCompletePendedPreOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)从工作线程。

如果微筛选器驱动程序需要维护其自身的每个实例取消安全队列未完成 I/O 操作要处理的它可以通过调用将设置此类队列[ *FltCbdqInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinitialize)在其*InstanceSetupCallback*例程并调用[ *FltCbdqInsertIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinsertio)其 preoperation 回调例程根据需要将 I/O 操作插入队列中。

筛选器管理器调用微筛选器驱动程序[ **postoperation 回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)例程在较低的筛选器驱动程序 （旧的筛选器和微筛选器驱动程序） 完成后完成的 I/O 操作正在处理。

在其 postoperation 回调例程，微筛选器驱动程序可以调用[ **FltDoCompletionProcessingWhenSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)以确保该完成处理工作都在安全的 irql 下完成。 或它可以根据需要通过调用进行排队的工作线程上的操作完成处理[ **FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)。 这样做之后，微筛选器驱动程序返回 FLT\_POSTOP\_详细\_处理\_从其 postoperation 回调例程所需停止筛选器管理器完成处理的 I/O 操作。 若要继续完成处理，微筛选器驱动程序调用[ **FltCompletePendedPostOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)从工作线程。

筛选器管理器提供对队列的"通用"工作项-工作项相关联的微筛选器驱动程序或微筛选器驱动程序实例，而非 I/O 操作的支持。 微筛选器驱动程序可以将工作项插入系统工作队列通过调用[ **FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem)。 此例程是类似于例程，如[ **ExQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exqueueworkitem); 例如，工作项 (通过调用分配[ **FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocategenericworkitem)) 可以重复使用。 但是， **FltQueueGenericWorkItem**是微筛选器驱动程序使用，更安全，因为筛选器管理器不允许微筛选器驱动程序或微筛选器驱动程序实例，卸载时仍在未完成的工作项处理。

筛选器管理器还提供对支持机会锁 (oplock) 操作。 对于 oplock 操作，微筛选器驱动程序可以使用为此类筛选器管理器例程[ **FltInitializeOplock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializeoplock)并[ **FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)，等效于**FsRtlInitializeOplock**并**FsRtlOplockFsctrl**文件系统和旧的筛选器驱动程序所使用的例程。

### <a name="span-idfiltermanagerroutinesforprocessingiooperationsspanspan-idfiltermanagerroutinesforprocessingiooperationsspanspan-idfiltermanagerroutinesforprocessingiooperationsspanfilter-manager-routines-for-processing-io-operations"></a><span id="Filter_Manager_Routines_for_Processing_I_O_Operations"></span><span id="filter_manager_routines_for_processing_i_o_operations"></span><span id="FILTER_MANAGER_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>用于处理 I/O 操作中筛选管理器例程

筛选器管理器提供了有关挂起的 I/O 中的以下支持例程[ **preoperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)并[ **postoperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)回调例程：

[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)

[**FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)

[**FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)

下面的例程用于 preoperation 和 postoperation 回调例程中的队列工作项：

[**FltAllocateDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)

[**FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocategenericworkitem)

[**FltFreeDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreedeferredioworkitem)

[**FltFreeGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreegenericworkitem)

[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)

[**FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem)

下面的例程提供取消安全队列支持：

[*FltCbdqDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqdisable)

[*FltCbdqEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqenable)

[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinitialize)

[*FltCbdqInsertIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinsertio)

[*FltCbdqRemoveIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqremoveio)

[*FltCbdqRemoveNextIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqremovenextio)

下面的例程提供 oplock 支持：

[*FltCheckOplock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcheckoplock)

[**FltCurrentBatchOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcurrentbatchoplock)

[**FltInitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializeoplock)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FltOplockIsFastIoPossible**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockisfastiopossible)

[**FltUninitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuninitializeoplock)

### <a name="span-idminifilterdrivercallbackroutinesforprocessingiooperationsspanspan-idminifilterdrivercallbackroutinesforprocessingiooperationsspanspan-idminifilterdrivercallbackroutinesforprocessingiooperationsspanminifilter-driver-callback-routines-for-processing-io-operations"></a><span id="Minifilter_Driver_Callback_Routines_for_Processing_I_O_Operations"></span><span id="minifilter_driver_callback_routines_for_processing_i_o_operations"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>微筛选器驱动程序用于处理 I/O 操作的回调例程

下面的回调例程都存储在[ **FLT\_操作\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_operation_registration)微筛选器驱动程序处理的 I/O 操作的每种类型的结构：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_POST_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)"><strong>PFLT_POST_OPERATION_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>PreOperation</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




