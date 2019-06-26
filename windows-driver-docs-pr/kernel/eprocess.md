---
title: Windows 内核不透明结构
description: Windows 内核不透明结构
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0babcca7994c19d37d40e0e30a06dd3bf6bb92c2
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393776"
---
# <a name="windows-kernel-opaque-structures"></a>Windows 内核不透明结构


下表包含 Windows 内核不透明结构：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>不透明结构</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>EPROCESS</strong></td>
<td><p><strong>EPROCESS</strong>结构是可作为进程的进程对象的不透明结构。</p>
<p>一些例程，如<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetprocesscreatetimequadpart" data-raw-source="[&lt;strong&gt;PsGetProcessCreateTimeQuadPart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)"> <strong>PsGetProcessCreateTimeQuadPart</strong></a>，使用<strong>EPROCESS</strong>来识别要操作的进程。 驱动程序可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess" data-raw-source="[&lt;strong&gt;PsGetCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)"> <strong>PsGetCurrentProcess</strong> </a>例程，以获取指向过程的对象的当前进程，并可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong></a>例程，以获取与指定句柄关联的进程对象的指针。 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress" data-raw-source="[&lt;strong&gt;PsInitialSystemProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)"> <strong>PsInitialSystemProcess</strong> </a>全局变量指向系统进程的进程对象。</p>
<p>请注意，将进程对象的对象管理器对象。 驱动程序应使用对象管理器例程如下所示<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)"> <strong>ObReferenceObject</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)"> <strong>ObDereferenceObject</strong> </a>维护的对象引用计数。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p><strong>ETHREAD</strong>结构是可作为一个线程的线程对象的不透明结构。</p>
<p>一些例程，如<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psissystemthread" data-raw-source="[&lt;strong&gt;PsIsSystemThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psissystemthread)"> <strong>PsIsSystemThread</strong></a>，使用<strong>ETHREAD</strong>来标识要在上运行的线程。 驱动程序可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetcurrentthread" data-raw-source="[&lt;strong&gt;PsGetCurrentThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetcurrentthread)"> <strong>PsGetCurrentThread</strong> </a>例程，以获取指向该线程的当前线程对象，并可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong></a>例程，以获取与指定句柄关联的线程对象的指针。</p>
<p>请注意，线程对象的对象管理器对象。 驱动程序应使用对象管理器例程如下所示<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)"> <strong>ObReferenceObject</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)"> <strong>ObDereferenceObject</strong> </a>维护的对象引用计数。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>EX_RUNDOWN_REF</strong></td>
<td><p><strong>EX_RUNDOWN_REF</strong>结构是不透明系统结构，其中包含有关状态的 run-down 保护关联的共享对象的信息。</p>
<pre class="syntax"><code>typedef struct _EX_RUNDOWN_REF {
  
  ...  // opaque
  
} EX_RUNDOWN_REF, *PEX_RUNDOWN_REF;</code></pre>
<p>所有的 run-down 保护例程需要一个指向<strong>EX_RUNDOWN_REF</strong>结构作为其第一个参数。 在此页的底部列出了这些例程。</p>
<p>有关详细信息，请参阅<a href="run-down-protection.md" data-raw-source="[Run-Down Protection](run-down-protection.md)">逐一介绍保护</a>。</p>
<p>标头：Wdm.h。 包括 wdm.h。</p></td>
</tr>
<tr class="even">
<td><strong>EX_TIMER</strong></td>
<td><p><strong>EX_TIMER</strong>结构是操作系统用于表示的不透明结构<strong>EX_TIMER</strong>计时器对象。</p>
<pre class="syntax"><code>typedef struct _EX_TIMER *PEX_TIMER;</code></pre>
<p>此结构的所有成员都是不透明的驱动程序。</p>
<p>以下<strong>Ex<em>Xxx</em>计时器</strong>例程需要一个指向系统分配<strong>EX_TIMER</strong>作为输入参数的结构：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer" data-raw-source="[&lt;strong&gt;ExSetTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)"><strong>ExSetTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer" data-raw-source="[&lt;strong&gt;ExCancelTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer)"><strong>ExCancelTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer" data-raw-source="[&lt;strong&gt;ExDeleteTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer)"><strong>ExDeleteTimer</strong></a></li>
</ul>
<p><strong>EX_TIMER</strong>-由操作系统创建基于的计时器对象。 若要获取此类计时器对象，驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer" data-raw-source="[&lt;strong&gt;ExAllocateTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)"> <strong>ExAllocateTimer</strong> </a>例程。 当不再需要此对象时，该驱动程序负责通过调用删除对象<strong>ExDeleteTimer</strong>。</p>
<p>有关详细信息，请参阅<a href="exxxxtimer-routines-and-ex-timer-objects.md" data-raw-source="[Ex&lt;em&gt;Xxx&lt;/em&gt;Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md)">Ex<em>Xxx</em>计时器例程和 EX_TIMER 对象</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p>一个<strong>FAST_MUTEX</strong>结构是表示一个快速的互斥体的不透明的数据结构。</p>
<p>一个<strong>FAST_MUTEX</strong>结构初始化由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializefastmutex" data-raw-source="[&lt;strong&gt;ExInitializeFastMutex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializefastmutex)"> <strong>ExInitializeFastMutex</strong> </a>例程。</p>
<p>有关快速互斥体的详细信息，请参阅<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">快速互斥锁和受保护的互斥体</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p><strong>IO_CSQ</strong>结构是用于指定驱动程序的取消安全 IRP 队列例程的不透明结构。 不能直接设置此结构的成员。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize" data-raw-source="[&lt;strong&gt;IoCsqInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize)"> <strong>IoCsqInitialize</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex" data-raw-source="[&lt;strong&gt;IoCsqInitializeEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex)"> <strong>IoCsqInitializeEx</strong> </a>初始化此结构。</p>
<p>有关如何使用取消安全 IRP 队列的概述，请参阅<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">取消安全 IRP 队列</a>。</p>
<p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统上可用。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p><strong>IO_CSQ_IRP_CONTEXT</strong>结构是不透明的数据结构，用于指定的驱动程序的取消安全 IRP 队列中 IRP 的 IRP 上下文。 它用作通过键<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp" data-raw-source="[&lt;strong&gt;IoCsqInsertIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)"> <strong>IoCsqInsertIrp</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex" data-raw-source="[&lt;strong&gt;IoCsqInsertIrpEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)"> <strong>IoCsqInsertIrpEx</strong></a>，并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp" data-raw-source="[&lt;strong&gt;IoCsqRemoveIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)"> <strong>IoCsqRemoveIrp</strong> </a>例程来标识特定 Irp 队列中的。</p>
<p>有关如何使用取消安全 IRP 队列的概述，请参阅<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">取消安全 IRP 队列</a>。</p>
<p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统上可用。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p><strong>IO_WORKITEM</strong>结构是描述系统工作线程的工作项的不透明结构。</p>
<p>驱动程序可以通过调用分配一个工作项<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)"> <strong>IoAllocateWorkItem</strong></a>。 或者，驱动程序可以分配其自己的缓冲区，然后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeworkitem" data-raw-source="[&lt;strong&gt;IoInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeworkitem)"> <strong>IoInitializeWorkItem</strong> </a>来初始化该缓冲区作为工作项。</p>
<p>分配的任何工作项<strong>IoAllocateWorkItem</strong>必须释放<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem" data-raw-source="[&lt;strong&gt;IoFreeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)"> <strong>IoFreeWorkItem</strong></a>。 任何情况下将初始化的内存<strong>IoInitializeWorkItem</strong>必须通过未初始化<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iouninitializeworkitem" data-raw-source="[&lt;strong&gt;IoUninitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iouninitializeworkitem)"> <strong>IoUninitializeWorkItem</strong> </a>可释放之前。</p>
<p>有关工作项的详细信息，请参阅<a href="system-worker-threads.md" data-raw-source="[System Worker Threads](system-worker-threads.md)">系统工作线程数</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_CALLBACK_RECORD</strong>结构是由不透明结构<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback)"> <strong>KeRegisterBugCheckCallback</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback)"> <strong>KeDeregisterBugCheckCallback</strong> </a>例程。</p>
<p><strong>KBUGCHECK_CALLBACK_RECORD</strong>结构用于由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>例程。</p>
<p>必须在常驻内存中，如非分页缓冲池分配结构。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>KeInitializeCallbackRecord</strong> </a>例程使用它之前初始化结构。</p>
<p>标头：Ntddk.h。 包括：Ntddk.h。</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>结构是由不透明结构<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>例程。</p>
<p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>结构用于由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>例程。</p>
<p>必须在常驻内存中，如非分页缓冲池分配结构。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>KeInitializeCallbackRecord</strong> </a>例程使用它之前初始化结构。</p>
<p>在 Microsoft Windows XP Service Pack 1 (SP1)、 Windows Server 2003 和更高版本的 Windows 操作系统上可用。</p>
<p>标头：Ntddk.h。 包括：Ntddk.h。</p></td>
</tr>
<tr class="odd">
<td><strong>KDPC</strong></td>
<td><p><strong>KDPC</strong>结构是表示 DPC 对象的不透明结构。 不能直接设置此结构的成员。 请参阅<a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">DPC 对象和 dpc 进行标记</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>KFLOATING_SAVE</strong></td>
<td><p><strong>KFLOATING_SAVE</strong>结构是一个不透明结构描述的浮点状态<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate" data-raw-source="[&lt;strong&gt;KeSaveFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate)"> <strong>KeSaveFloatingPointState</strong> </a>保存的例程。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate" data-raw-source="[&lt;strong&gt;KeRestoreFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate)"> <strong>KeRestoreFloatingPointState</strong> </a>要还原的浮点状态。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>KGUARDED_MUTEX</strong></td>
<td><p><strong>KGUARDED_MUTEX</strong>结构是表示受保护的互斥体的不透明结构。</p>
<p>使用<strong>KeInitializeGuardedMutex</strong>来初始化<strong>KGUARDED_MUTEX</strong>与受保护的互斥体的结构。</p>
<p>受保护的互斥体必须通过非页面缓冲池分配。</p>
<p>有关受保护的互斥体的详细信息，请参阅<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">快速互斥锁和受保护的互斥体</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>KINTERRUPT</strong></td>
<td><p>一个<strong>KINTERRUPT</strong>结构是表示中断到系统的不透明结构。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex" data-raw-source="[&lt;strong&gt;IoConnectInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)"><strong>IoConnectInterruptEx</strong> </a>提供一个指针指向<strong>KINTERRUPT</strong>中断时该驱动程序注册的结构<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)"> <em>InterruptService</em> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine" data-raw-source="[&lt;em&gt;InterruptMessageService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)"> <em>InterruptMessageService</em> </a>例程。 驱动程序使用此指针时获取或释放中断的中断自旋锁。 驱动程序还使用此指针时注销<em>InterruptService</em>例程。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p><strong>KLOCK_QUEUE_HANDLE</strong>结构是描述排队的旋转锁的不透明结构。 驱动程序分配了<strong>KLOCK_QUEUE_HANDLE</strong>结构，并将其传递给<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>并<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"> <strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong> </a>获取排队的自旋锁。 这些例程初始化该结构以表示排队的自旋锁。 该驱动程序将向此结构传递<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"> <strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong> </a>当释放自旋锁。</p>
<p>有关详细信息，请参阅<a href="queued-spin-locks.md" data-raw-source="[Queued Spin Locks](queued-spin-locks.md)">排队旋转锁</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>KTIMER</strong></td>
<td><p><strong>KTIMER</strong>结构是表示计时器对象的不透明结构。 不能直接设置此结构的成员。 有关详细信息，请参阅<a href="timer-objects-and-dpcs.md" data-raw-source="[Timer Objects and DPCs](timer-objects-and-dpcs.md)">计时器对象和 dpc 进行标记</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>LOOKASIDE_LIST_EX</strong></td>
<td><p><strong>LOOKASIDE_LIST_EX</strong>结构描述后备链列表。</p>
<pre class="syntax"><code>typedef struct _LOOKASIDE_LIST_EX {
  ...  // opaque
} LOOKASIDE_LIST_EX, *PLOOKASIDE_LIST_EX;</code></pre>
<p>后备链列表是驱动程序可以在本地管理为了减少对系统的分配例程和调用，从而为固定大小缓冲区的池，提高性能。 缓冲区是统一的大小和存储为后备链列表中的条目。</p>
<p>驱动程序应将<strong>LOOKASIDE_LIST_EX</strong>视为不透明结构。 可移植且可互操作与其他驱动程序，不可能保持驱动程序访问结构成员或这些成员的位置具有依赖项。</p>
<p>另请参阅下面列出了使用此结构的例程。</p>
<p>有关旁视列表的详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">使用后备链列表</a>。</p>
<p>在 64 位平台上，此结构必须是 16 字节对齐。</p>
<p>支持与 Windows Vista 一起启动。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>NPAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>NPAGED_LOOKASIDE_LIST</strong>结构是描述分配从非分页缓冲池的固定大小缓冲区的后备链列表的不透明结构。 系统将创建新的项，并销毁根据列表上未使用的条目。 对于固定大小的缓冲区，使用后备链列表是快于直接分配的内存。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializeNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)"> <strong>ExInitializeNPagedLookasideList</strong> </a>初始化后备链列表。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromnpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromnpagedlookasidelist)"> <strong>ExAllocateFromNPagedLookasideList</strong> </a>来分配缓冲区从列表中，并且<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetonpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetonpagedlookasidelist)"> <strong>ExFreeToNPagedLookasideList</strong> </a>返回到列表的缓冲区。</p>
<p>驱动程序必须始终显式地释放它们在卸载之前创建的任何后备链列表。 严重的编程错误，否则它。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeleteNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist)"> <strong>ExDeleteNPagedLookasideList</strong> </a>来释放列表。</p>
<p>驱动程序还可以为页面缓冲池使用后备链列表。 从 Windows 2000 <strong>PAGED_LOOKASIDE_LIST</strong>结构描述包含分页的缓冲区的后备链列表。 从 Windows Vista 开始<strong>LOOKASIDE_LIST_EX</strong>结构可以描述包含分页或非分页缓冲区的后备链列表。 有关详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">使用后备链列表</a>。</p>
<p>在 64 位平台上，此结构必须是 16 字节对齐。</p>
<p>支持从 Windows 2000 开始。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong>是指定的句柄的对象类型的不透明结构。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong></a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>PAGED_LOOKASIDE_LIST</strong>结构是描述固定大小缓冲区从页面缓冲池分配的后备链列表的不透明结构。 系统将创建新的项，并销毁根据列表上未使用的条目。 对于固定大小的缓冲区，使用后备链列表是快于直接分配的内存。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)"> <strong>ExInitializePagedLookasideList</strong> </a>初始化后备链列表。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefrompagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefrompagedlookasidelist)"> <strong>ExAllocateFromPagedLookasideList</strong> </a>来分配缓冲区从列表中，并且<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetopagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetopagedlookasidelist)"> <strong>ExFreeToPagedLookasideList</strong> </a>返回到列表的缓冲区。</p>
<p>驱动程序必须始终显式地释放它们在卸载之前创建的任何后备链列表。 严重的编程错误，否则它。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeletePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist)"> <strong>ExDeletePagedLookasideList</strong> </a>来释放列表。</p>
<p>驱动程序还可以为非分页缓冲池使用后备链列表。 从 Windows 2000 <strong>NPAGED_LOOKASIDE_LIST</strong>结构描述的旁路列表包含非分页的缓冲区。 从 Windows Vista 开始<strong>LOOKASIDE_LIST_EX</strong>结构可以描述包含分页或非分页缓冲区的后备链列表。 有关详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">使用后备链列表</a>。</p>
<p>在 64 位平台上，此结构必须是 16 字节对齐。</p>
<p>支持从 Windows 2000 开始。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>RTL_BITMAP</strong></td>
<td><p><strong>RTL_BITMAP</strong>结构是描述位图的不透明结构。</p>
<pre class="syntax"><code>typedef struct _RTL_BITMAP {
  // opaque
} RTL_BITMAP, *PRTL_BITMAP;</code></pre>
<p>并不直接访问此结构的成员。 存在有关成员位置的依赖关系或，访问成员值直接可能不再与未来版本的 Windows 操作系统兼容的驱动程序。</p>
<p><strong>RTL_BITMAP</strong>结构用作任意长度的常规用途、 一维位图的标头。 驱动程序可以使用这种位图作为经济的方法来跟踪一组可重用的项。 例如，文件系统可以使用位图来跟踪哪些群集和已分配的硬盘上的扇区来保存文件数据。</p>
<p>有关一系列<strong>Rtl<em>Xxx</em></strong> 使用的例程<strong>RTL_BITMAP</strong>结构，请参阅以下部分。 这些调用方<strong>Rtl<em>Xxx</em></strong> 例程负责分配的存储<strong>RTL_BITMAP</strong>结构并且缓冲区包含位图。 此缓冲区必须以在内存中的 4 字节边界上，并且必须是长度在四个字节的倍数。 位图的缓冲区的开头开始，但可以包含任意数量的位将分配的缓冲区中容纳不下。</p>
<p>提供之前<strong>RTL_BITMAP</strong>作为参数的结构<strong>Rtl<em>Xxx</em></strong> 例程，调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitializebitmap" data-raw-source="[&lt;strong&gt;RtlInitializeBitMap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitializebitmap)"> <strong>RtlInitializeBitMap</strong></a>例程初始化结构。 此例程的输入的参数是位图的指向包含位图，并以位为单位的大小的缓冲区的指针。 <strong>RtlInitializeBitMap</strong>不会更改此缓冲区的内容。</p>
<p>如果调用方分配的存储<strong>RTL_BITMAP</strong>结构和分页内存中的位图，调用方必须在 IRQL 运行&lt;= APC_LEVEL 时它将指针传递给此结构作为参数任一<strong>Rtl<em>Xxx</em></strong> 另请参阅部分中列出的例程。 如果调用方分配存储，从非分页内存 （或，也可以说锁定的分页内存），可以运行的任何 irql 的调用方调用时<strong>Rtl<em>Xxx</em></strong> 例程。</p>
<p>支持在 Windows 2000 和更高版本的 Windows。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p><strong>RTL_RUN_ONCE</strong>结构是将存储一次性初始化的信息的不透明结构。</p>
<p>驱动程序必须通过调用初始化此结构<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceinitialize" data-raw-source="[&lt;strong&gt;RtlRunOnceInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceinitialize)"> <strong>RtlRunOnceInitialize</strong> </a>然后再将它传递到任何其他例程<strong>RtlRunOnce<em>Xxx</em></strong> 例程。</p>
<p>仅在 Windows Vista 和更高版本的 Windows 操作系统上可用。</p>
<p>标头：Ntddk.h。 包括：Ntddk.h。</p></td>
</tr>
<tr class="odd">
<td><strong>SECURITY_SUBJECT_CONTEXT</strong></td>
<td><p><strong>SECURITY_SUBJECT_CONTEXT</strong>结构是表示在其中某一特定操作正在进行的安全上下文的不透明结构。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>SLIST_HEADER</strong></td>
<td><p><strong>SLIST_HEADER</strong>结构是可作为已编序的单向链接列表的标头的不透明结构。 有关详细信息，请参阅<a href="singly-and-doubly-linked-lists.md" data-raw-source="[Singly and Doubly Linked Lists](singly-and-doubly-linked-lists.md)">单向和双向链接中列出了</a>。</p>
<p>在 64 位平台上<strong>SLIST_HEADER</strong>结构必须是 16 字节对齐。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>XSTATE_SAVE</strong></td>
<td><p><strong>XSTATE_SAVE</strong>结构是描述的内核模式驱动程序将保存并还原的扩展的处理器状态信息的不透明结构。</p>
<pre class="syntax"><code>typedef struct _XSTATE_SAVE {
  ...  // opaque
} XSTATE_SAVE, *PXSTATE_SAVE;</code></pre>
<p>所有成员都是不透明的。</p>
<p>此结构可供<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesaveextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeSaveExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesaveextendedprocessorstate)"> <strong>KeSaveExtendedProcessorState</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestoreextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeRestoreExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestoreextendedprocessorstate)"> <strong>KeRestoreExtendedProcessorState</strong> </a>例程。</p>
<p>Windows 7 和更高版本的 Windows 操作系统支持。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))  
[**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))  
[**ExAllocateFromLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromlookasidelistex)  
[**ExAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromnpagedlookasidelist)  
[**ExAllocateFromPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefrompagedlookasidelist)  
[**ExAllocateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)  
[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist)  
[**ExFreeToPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetopagedlookasidelist)  
[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)  
[**ExCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer)  
[**ExDeleteLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletelookasidelistex)  
[**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist)  
[**ExDeleteTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer)  
[**ExFlushLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exflushlookasidelistex)  
[**ExFreeToLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetolookasidelistex)  
[**ExFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetonpagedlookasidelist)  
[**ExInitializeLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializelookasidelistex)  
[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)  
[**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializeslisthead)  
[**ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedflushslist)  
[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpopentryslist)  
[**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpushentryslist)  
[**ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exquerydepthslist)  
[**ExReleaseFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545549(v=vs.85))  
[**ExReleaseFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545567(v=vs.85))  
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)  
[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))  
[*ExTimerCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ext_callback)  
[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)  
[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)  
[**IoCsqInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize)  
[**IoCsqInitializeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex)  
[**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)  
[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)  
[**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)  
[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterruptex)  
[**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)  
[**IoInitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeworkitem)  
[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)  
[**IoUninitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iouninitializeworkitem)  
[**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))  
[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))  
[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))  
[**KeAcquireInterruptSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))  
[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kecanceltimer)  
[**KeInitializeCallbackRecord**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)  
[**KeInitializeGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeguardedmutex)  
[**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimer)  
[**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimerex)  
[**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereadstatetimer)  
[**KeRestoreExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestoreextendedprocessorstate)  
[**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesaveextendedprocessorstate)  
[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)  
[**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)  
[**KeDeregisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback)  
[**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)  
[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)  
[**KeRegisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback)  
[**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)  
[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseguardedmutexunsafe)  
[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)  
[**KeReleaseInterruptSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinterruptspinlock)  
[**KeRestoreFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate)  
[**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate)  
[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)  
[*LookasideListAllocateEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-allocate_function_ex)  
[*LookasideListFreeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-free_function_ex)  
[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)  
[**PsGetCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)  
[**PsGetProcessCreateTimeQuadPart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)  
[**PsInitialSystemProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)  
[**PsIsSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psissystemthread)  
[**RtlRunOnceBeginInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunoncebegininitialize)  
[**RtlRunOnceComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunoncecomplete)  
[**RtlRunOnceExecuteOnce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceexecuteonce)  
[**RtlRunOnceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceinitialize)  
[*RunOnceInitialization*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-rtl_run_once_init_fn)  
[Run-Down 保护](run-down-protection.md)  
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck)  
[**SeAssignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seassignsecurity)  
[**SeAssignSecurityEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seassignsecurityex)  



