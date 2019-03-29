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
ms.openlocfilehash: 50414b051475a1daeb877b5b6f65565d8f25b2f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566405"
---
# <a name="processing-io-operations"></a>处理 I/O 操作


筛选器管理器可简化微筛选器驱动程序处理 I/O 操作。 与传统的筛选器驱动程序，它必须正确地将所有 I/O 请求都传递到下一个较低的驱动程序和旧的筛选器驱动程序执行任何工作是否正确处理挂起的请求、 同步和 I/O 完成与请求相关，微筛选器驱动程序仅对必须处理的 I/O 操作的寄存器。

对于给定的 I/O 操作，筛选器管理器调用仅微筛选器驱动程序的已注册[ **preoperation 回调**](https://msdn.microsoft.com/library/windows/hardware/ff551109)例行为该操作。 筛选器管理器还可以处理某些 IRP 维护任务代表微筛选器驱动程序，如将参数复制到下一步的堆栈位置和传播 IRP **PendingReturned**标志。

在其 preoperation 回调例程中，微筛选器驱动程序执行任何处理所需的 I/O 操作和指示该怎么办呢 IRP 到通过从其 preoperation 回调例程返回适当的值。 例如，要将转发到下一步低驱动程序而无需完成例程 IRP，微筛选器驱动程序返回 FLT\_PREOP\_成功\_否\_回调; 若要执行完成例程 (使用相同的操作微筛选器驱动程序的 postoperation 回调例程的 I/O 操作），微筛选器驱动程序将返回 FLT\_PREOP\_成功\_WITH\_回调。

在其 preoperation 回调例程中，微筛选器驱动程序可以排入队列工作线程上的操作根据需要通过调用[ **FltQueueDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543449)。 这样做之后，微筛选器驱动程序返回 FLT\_PREOP\_PENDING 从其 preoperation 回调例程，以指示 I/O 操作处于挂起状态，并且微筛选器驱动程序负责完成或恢复的处理该请求。 若要继续处理微筛选器驱动程序调用[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913)从工作线程。

如果微筛选器驱动程序需要维护其自身的每个实例取消安全队列未完成 I/O 操作要处理的它可以通过调用将设置此类队列[ *FltCbdqInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff541802)在其*InstanceSetupCallback*例程并调用[ *FltCbdqInsertIo* ](https://msdn.microsoft.com/library/windows/hardware/ff541815)其 preoperation 回调例程根据需要将 I/O 操作插入队列中。

筛选器管理器调用微筛选器驱动程序[ **postoperation 回调**](https://msdn.microsoft.com/library/windows/hardware/ff551107)例程在较低的筛选器驱动程序 （旧的筛选器和微筛选器驱动程序） 完成后完成的 I/O 操作正在处理。

在其 postoperation 回调例程，微筛选器驱动程序可以调用[ **FltDoCompletionProcessingWhenSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff542047)以确保该完成处理工作都在安全的 irql 下完成。 或它可以根据需要通过调用进行排队的工作线程上的操作完成处理[ **FltQueueDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543449)。 这样做之后，微筛选器驱动程序返回 FLT\_POSTOP\_详细\_处理\_从其 postoperation 回调例程所需停止筛选器管理器完成处理的 I/O 操作。 若要继续完成处理，微筛选器驱动程序调用[ **FltCompletePendedPostOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541897)从工作线程。

筛选器管理器提供对队列的"通用"工作项-工作项相关联的微筛选器驱动程序或微筛选器驱动程序实例，而非 I/O 操作的支持。 微筛选器驱动程序可以将工作项插入系统工作队列通过调用[ **FltQueueGenericWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543452)。 此例程是类似于例程，如[ **ExQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff540216); 例如，工作项 (通过调用分配[ **FltAllocateGenericWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff541749)) 可以重复使用。 但是， **FltQueueGenericWorkItem**是微筛选器驱动程序使用，更安全，因为筛选器管理器不允许微筛选器驱动程序或微筛选器驱动程序实例，卸载时仍在未完成的工作项处理。

筛选器管理器还提供对支持机会锁 (oplock) 操作。 对于 oplock 操作，微筛选器驱动程序可以使用为此类筛选器管理器例程[ **FltInitializeOplock** ](https://msdn.microsoft.com/library/windows/hardware/ff543289)并[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)，等效于**FsRtlInitializeOplock**并**FsRtlOplockFsctrl**文件系统和旧的筛选器驱动程序所使用的例程。

### <a name="span-idfiltermanagerroutinesforprocessingiooperationsspanspan-idfiltermanagerroutinesforprocessingiooperationsspanspan-idfiltermanagerroutinesforprocessingiooperationsspanfilter-manager-routines-for-processing-io-operations"></a><span id="Filter_Manager_Routines_for_Processing_I_O_Operations"></span><span id="filter_manager_routines_for_processing_i_o_operations"></span><span id="FILTER_MANAGER_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>用于处理 I/O 操作中筛选管理器例程

筛选器管理器提供了有关挂起的 I/O 中的以下支持例程[ **preoperation** ](https://msdn.microsoft.com/library/windows/hardware/ff551109)并[ **postoperation** ](https://msdn.microsoft.com/library/windows/hardware/ff551107)回调例程：

[**FltCompletePendedPostOperation**](https://msdn.microsoft.com/library/windows/hardware/ff541897)

[**FltCompletePendedPreOperation**](https://msdn.microsoft.com/library/windows/hardware/ff541913)

[**FltDoCompletionProcessingWhenSafe**](https://msdn.microsoft.com/library/windows/hardware/ff542047)

下面的例程用于 preoperation 和 postoperation 回调例程中的队列工作项：

[**FltAllocateDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff541720)

[**FltAllocateGenericWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff541749)

[**FltFreeDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff542955)

[**FltFreeGenericWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff542971)

[**FltQueueDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543449)

[**FltQueueGenericWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543452)

下面的例程提供取消安全队列支持：

[*FltCbdqDisable*](https://msdn.microsoft.com/library/windows/hardware/ff541796)

[*FltCbdqEnable*](https://msdn.microsoft.com/library/windows/hardware/ff541799)

[*FltCbdqInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff541802)

[*FltCbdqInsertIo*](https://msdn.microsoft.com/library/windows/hardware/ff541815)

[*FltCbdqRemoveIo*](https://msdn.microsoft.com/library/windows/hardware/ff541821)

[*FltCbdqRemoveNextIo*](https://msdn.microsoft.com/library/windows/hardware/ff541825)

下面的例程提供 oplock 支持：

[*FltCheckOplock*](https://msdn.microsoft.com/library/windows/hardware/ff541844)

[**FltCurrentBatchOplock**](https://msdn.microsoft.com/library/windows/hardware/ff541946)

[**FltInitializeOplock**](https://msdn.microsoft.com/library/windows/hardware/ff543289)

[**FltOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff543398)

[**FltOplockIsFastIoPossible**](https://msdn.microsoft.com/library/windows/hardware/ff543404)

[**FltUninitializeOplock**](https://msdn.microsoft.com/library/windows/hardware/ff544598)

### <a name="span-idminifilterdrivercallbackroutinesforprocessingiooperationsspanspan-idminifilterdrivercallbackroutinesforprocessingiooperationsspanspan-idminifilterdrivercallbackroutinesforprocessingiooperationsspanminifilter-driver-callback-routines-for-processing-io-operations"></a><span id="Minifilter_Driver_Callback_Routines_for_Processing_I_O_Operations"></span><span id="minifilter_driver_callback_routines_for_processing_i_o_operations"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>微筛选器驱动程序用于处理 I/O 操作的回调例程

下面的回调例程都存储在[ **FLT\_操作\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544668)微筛选器驱动程序处理的 I/O 操作的每种类型的结构：

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551107" data-raw-source="[&lt;strong&gt;PFLT_POST_OPERATION_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551107)"><strong>PFLT_POST_OPERATION_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>PreOperation</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551109" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551109)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




