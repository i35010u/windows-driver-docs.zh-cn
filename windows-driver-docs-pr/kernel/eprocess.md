---
title: Windows 内核不透明结构
description: Windows 内核不透明结构
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba5d30b1a937505bd2d8dc8e27e15c56690e3c9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838710"
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
<td><p><strong>EPROCESS</strong>结构是一个不透明的结构，它充当进程的进程对象。</p>
<p>某些例程（如<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetprocesscreatetimequadpart" data-raw-source="[&lt;strong&gt;PsGetProcessCreateTimeQuadPart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)"><strong>PsGetProcessCreateTimeQuadPart</strong></a>）使用<strong>EPROCESS</strong>标识操作的进程。 驱动程序可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess" data-raw-source="[&lt;strong&gt;PsGetCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)"><strong>PsGetCurrentProcess</strong></a>例程获取指向当前进程的进程对象的指针，并可使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a>例程获取指向与指定的关联的进程对象的指针。柄. <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress" data-raw-source="[&lt;strong&gt;PsInitialSystemProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)"><strong>PsInitialSystemProcess</strong></a>全局变量指向系统进程的进程对象。</p>
<p>请注意，进程对象是对象管理器对象。 驱动程序应使用对象管理器例程（如<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)"><strong>ObDereferenceObject</strong></a> ）来维护对象的引用计数。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p><strong>ETHREAD</strong>结构是一个不透明的结构，它充当线程的线程对象。</p>
<p>某些例程（如<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psissystemthread" data-raw-source="[&lt;strong&gt;PsIsSystemThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psissystemthread)"><strong>PsIsSystemThread</strong></a>）使用<strong>ETHREAD</strong>标识要在其上操作的线程。 驱动程序可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetcurrentthread" data-raw-source="[&lt;strong&gt;PsGetCurrentThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetcurrentthread)"><strong>PsGetCurrentThread</strong></a>例程获取指向当前线程的线程对象的指针，并可使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a>例程获取指向与指定的关联的线程对象柄.</p>
<p>请注意，线程对象是对象管理器对象。 驱动程序应使用对象管理器例程（如<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)"><strong>ObDereferenceObject</strong></a> ）来维护对象的引用计数。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>EX_RUNDOWN_REF</strong></td>
<td><p><strong>EX_RUNDOWN_REF</strong>结构是一个不透明的系统结构，其中包含有关关联共享对象的运行时保护状态的信息。</p>
<pre class="syntax"><code>typedef struct _EX_RUNDOWN_REF {
  
  ...  // opaque
  
} EX_RUNDOWN_REF, *PEX_RUNDOWN_REF;</code></pre>
<p>运行时保护例程会将指向<strong>EX_RUNDOWN_REF</strong>结构的指针作为其第一个参数。 此页的底部列出了这些例程。</p>
<p>有关详细信息，请参阅<a href="run-down-protection.md" data-raw-source="[Run-Down Protection](run-down-protection.md)">运行时保护</a>。</p>
<p>标头： Wdm .h。 包括 Wdm。</p></td>
</tr>
<tr class="even">
<td><strong>EX_TIMER</strong></td>
<td><p><strong>EX_TIMER</strong>结构是由操作系统用来表示<strong>EX_TIMER</strong>计时器对象的不透明结构。</p>
<pre class="syntax"><code>typedef struct _EX_TIMER *PEX_TIMER;</code></pre>
<p>此结构中的所有成员对驱动程序都不透明。</p>
<p>以下<strong>Ex<em>Xxx</em>计时器</strong>例程需要一个指向系统分配的<strong>EX_TIMER</strong>结构的指针作为输入参数：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer" data-raw-source="[&lt;strong&gt;ExSetTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)"><strong>ExSetTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer" data-raw-source="[&lt;strong&gt;ExCancelTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer)"><strong>ExCancelTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer" data-raw-source="[&lt;strong&gt;ExDeleteTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer)"><strong>ExDeleteTimer</strong></a></li>
</ul>
<p>基于<strong>EX_TIMER</strong>的计时器对象由操作系统创建。 若要获取此类计时器对象，驱动程序将调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer" data-raw-source="[&lt;strong&gt;ExAllocateTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)"><strong>ExAllocateTimer</strong></a>例程。 当不再需要此对象时，驱动程序将负责通过调用<strong>ExDeleteTimer</strong>来删除该对象。</p>
<p>有关详细信息，请参阅<a href="exxxxtimer-routines-and-ex-timer-objects.md" data-raw-source="[Ex&lt;em&gt;Xxx&lt;/em&gt;Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md)">Ex<em>Xxx</em>TIMER 例程和 EX_TIMER 对象</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p><strong>FAST_MUTEX</strong>结构是表示快速 MUTEX 的不透明数据结构。</p>
<p><strong>FAST_MUTEX</strong>结构由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializefastmutex" data-raw-source="[&lt;strong&gt;ExInitializeFastMutex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializefastmutex)"><strong>ExInitializeFastMutex</strong></a>例程初始化。</p>
<p>有关快速 mutex 的详细信息，请参阅<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">快速互斥体和受保护的 mutex</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p><strong>IO_CSQ</strong>结构是一个不透明的结构，用于指定驱动程序的取消安全 IRP 队列例程。 请勿直接设置此结构的成员。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize" data-raw-source="[&lt;strong&gt;IoCsqInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize)"><strong>IoCsqInitialize</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex" data-raw-source="[&lt;strong&gt;IoCsqInitializeEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex)"><strong>IoCsqInitializeEx</strong></a>初始化此结构。</p>
<p>有关如何使用取消安全 IRP 队列的概述，请参阅<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">取消安全 Irp 队列</a>。</p>
<p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统上可用。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p><strong>IO_CSQ_IRP_CONTEXT</strong>结构是一种不透明的数据结构，用于为驱动程序的取消安全 irp 队列中的 IRP 指定 irp 上下文。 它用作<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp" data-raw-source="[&lt;strong&gt;IoCsqInsertIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)"><strong>IoCsqInsertIrp</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex" data-raw-source="[&lt;strong&gt;IoCsqInsertIrpEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)"><strong>IoCsqInsertIrpEx</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp" data-raw-source="[&lt;strong&gt;IoCsqRemoveIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)"><strong>IoCsqRemoveIrp</strong></a>例程的键，用于标识队列中的特定 irp。</p>
<p>有关如何使用取消安全 IRP 队列的概述，请参阅<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">取消安全 Irp 队列</a>。</p>
<p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统上可用。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p><strong>IO_WORKITEM</strong>结构是描述系统工作线程的工作项的不透明结构。</p>
<p>驱动程序可以通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)"><strong>IoAllocateWorkItem</strong></a>来分配工作项。 或者，驱动程序可以分配其自己的缓冲区，然后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem" data-raw-source="[&lt;strong&gt;IoInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem)"><strong>IoInitializeWorkItem</strong></a>将该缓冲区初始化为一个工作项。</p>
<p><strong>IoAllocateWorkItem</strong>分配的任何工作项必须由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem" data-raw-source="[&lt;strong&gt;IoFreeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)"><strong>IoFreeWorkItem</strong></a>释放。 <strong>IoInitializeWorkItem</strong>初始化的任何内存必须由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem" data-raw-source="[&lt;strong&gt;IoUninitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem)"><strong>IoUninitializeWorkItem</strong></a>进行初始化，然后才能释放。</p>
<p>有关工作项的详细信息，请参阅<a href="system-worker-threads.md" data-raw-source="[System Worker Threads](system-worker-threads.md)">系统工作线程</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_CALLBACK_RECORD</strong>结构是由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback)"><strong>KeRegisterBugCheckCallback</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckcallback)"><strong>KeDeregisterBugCheckCallback</strong></a>例程使用的不透明结构。</p>
<p><strong>KBUGCHECK_CALLBACK_RECORD</strong>结构用于通过<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)"><strong>KeRegisterBugCheckReasonCallback</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"><strong>KeDeregisterBugCheckReasonCallback</strong></a>例程进行记帐。</p>
<p>此结构必须在常驻内存（如非分页池）中分配。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>KeInitializeCallbackRecord</strong></a>例程来初始化结构，然后再使用它。</p>
<p>标头： Ntddk。 包括： Ntddk。</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>结构是由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)"><strong>KeRegisterBugCheckReasonCallback</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"><strong>KeDeregisterBugCheckReasonCallback</strong></a>例程使用的不透明结构。</p>
<p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>结构用于通过<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)"><strong>KeRegisterBugCheckReasonCallback</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"><strong>KeDeregisterBugCheckReasonCallback</strong></a>例程进行记帐。</p>
<p>此结构必须在常驻内存（如非分页池）中分配。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>KeInitializeCallbackRecord</strong></a>例程来初始化结构，然后再使用它。</p>
<p>在 Microsoft Windows XP Service Pack 1 （SP1）、Windows Server 2003 和更高版本的 Windows 操作系统上可用。</p>
<p>标头： Ntddk。 包括： Ntddk。</p></td>
</tr>
<tr class="odd">
<td><strong>KDPC</strong></td>
<td><p><strong>KDPC</strong>结构是表示 DPC 对象的不透明结构。 请勿直接设置此结构的成员。 请参阅<a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">Dpc 对象和 dpc</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>KFLOATING_SAVE</strong></td>
<td><p><strong>KFLOATING_SAVE</strong>结构是一个不透明的结构，描述<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate" data-raw-source="[&lt;strong&gt;KeSaveFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)"><strong>KeSaveFloatingPointState</strong></a>例程保存的浮点状态。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate" data-raw-source="[&lt;strong&gt;KeRestoreFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)"><strong>KeRestoreFloatingPointState</strong></a>还原浮点状态。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>KGUARDED_MUTEX</strong></td>
<td><p><strong>KGUARDED_MUTEX</strong>结构是表示受保护的 MUTEX 的不透明结构。</p>
<p>使用<strong>KeInitializeGuardedMutex</strong>将<strong>KGUARDED_MUTEX</strong>结构初始化为受保护的 MUTEX。</p>
<p>必须从非分页池分配受保护的互斥体。</p>
<p>有关受保护的 mutex 的详细信息，请参阅<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">快速互斥体和受保护的 mutex</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>KINTERRUPT</strong></td>
<td><p><strong>KINTERRUPT</strong>结构是表示系统中断的不透明结构。</p>
<p>当驱动程序注册<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)"><em>InterruptService</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine" data-raw-source="[&lt;em&gt;InterruptMessageService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)"><em>InterruptMessageService</em></a>例程时， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex" data-raw-source="[&lt;strong&gt;IoConnectInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)"><strong>IoConnectInterruptEx</strong></a>提供了一个指向中断的<strong>KINTERRUPT</strong>结构的指针。 驱动程序在获取或释放中断的中断自旋锁时使用此指针。 该驱动程序还在取消注册<em>InterruptService</em>例程时使用此指针。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p><strong>KLOCK_QUEUE_HANDLE</strong>结构是描述排队自旋锁的不透明结构。 此驱动程序分配<strong>KLOCK_QUEUE_HANDLE</strong>结构，并将其传递给<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>和<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a>以获取排队的旋转锁。 这些例程将初始化结构，以表示排队的自旋锁。 当释放旋转锁时，驱动程序将该结构传递给<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a> 。</p>
<p>有关详细信息，请参阅<a href="queued-spin-locks.md" data-raw-source="[Queued Spin Locks](queued-spin-locks.md)">排队自旋锁</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>KTIMER</strong></td>
<td><p><strong>KTIMER</strong>结构是表示 timer 对象的不透明结构。 请勿直接设置此结构的成员。 有关详细信息，请参阅<a href="timer-objects-and-dpcs.md" data-raw-source="[Timer Objects and DPCs](timer-objects-and-dpcs.md)">Timer 对象和 dpc</a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>LOOKASIDE_LIST_EX</strong></td>
<td><p><strong>LOOKASIDE_LIST_EX</strong>结构描述了后备链表列表。</p>
<pre class="syntax"><code>typedef struct _LOOKASIDE_LIST_EX {
  ...  // opaque
} LOOKASIDE_LIST_EX, *PLOOKASIDE_LIST_EX;</code></pre>
<p>后备链表列表是固定大小缓冲区的池，驱动程序可以在本地进行管理，以减少对系统分配例程的调用次数，进而提高性能。 缓冲区的大小一致，并存储为后备链表列表中的条目。</p>
<p>驱动程序应将<strong>LOOKASIDE_LIST_EX</strong>结构视为不透明。 访问结构成员或对这些成员位置具有依赖关系的驱动程序，可能不会与其他驱动程序保持可移植性和互操作性。</p>
<p>下面的 "另请参见" 部分包含使用此结构的例程的列表。</p>
<p>有关后备链表列表的详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">使用后备链表列表</a>。</p>
<p>在64位平台上，此结构必须为16字节对齐。</p>
<p>从 Windows Vista 开始支持。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>NPAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>NPAGED_LOOKASIDE_LIST</strong>结构是描述从非分页池分配的固定大小缓冲区的后备链表列表的不透明结构。 系统会根据需要创建新条目并销毁列表中未使用的条目。 对于固定大小的缓冲区，使用后备链表列表比直接分配内存更快。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializeNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)"><strong>ExInitializeNPagedLookasideList</strong></a>初始化后备链表列表。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist)"><strong>ExAllocateFromNPagedLookasideList</strong></a>从列表中分配缓冲区，并使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)"><strong>ExFreeToNPagedLookasideList</strong></a>将缓冲区返回到列表。</p>
<p>在卸载之前，驱动程序必须始终显式释放其创建的所有后备链表列表。 否则，会出现严重的编程错误。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeleteNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)"><strong>ExDeleteNPagedLookasideList</strong></a>释放列表。</p>
<p>驱动程序还可以使用页面缓冲池的后备链表列表。 从 Windows 2000 开始， <strong>PAGED_LOOKASIDE_LIST</strong>结构描述了包含分页缓冲区的后备链表列表。 从 Windows Vista 开始， <strong>LOOKASIDE_LIST_EX</strong>结构可以描述包含分页或非分页缓冲区的后备链表列表。 有关详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">Using 后备链表 Lists</a>。</p>
<p>在64位平台上，此结构必须为16字节对齐。</p>
<p>支持从 Windows 2000 开始。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong>是不透明的结构，它指定句柄的对象类型。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a>。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>PAGED_LOOKASIDE_LIST</strong>结构是一种不透明结构，描述从分页池分配的固定大小缓冲区的后备链表列表。 系统会根据需要创建新条目并销毁列表中未使用的条目。 对于固定大小的缓冲区，使用后备链表列表比直接分配内存更快。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)"><strong>ExInitializePagedLookasideList</strong></a>初始化后备链表列表。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)"><strong>ExAllocateFromPagedLookasideList</strong></a>从列表中分配缓冲区，并使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)"><strong>ExFreeToPagedLookasideList</strong></a>将缓冲区返回到列表。</p>
<p>在卸载之前，驱动程序必须始终显式释放其创建的所有后备链表列表。 否则，会出现严重的编程错误。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeletePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)"><strong>ExDeletePagedLookasideList</strong></a>释放列表。</p>
<p>驱动程序还可以使用非分页池的后备链表列表。 从 Windows 2000 开始， <strong>NPAGED_LOOKASIDE_LIST</strong>结构描述了包含非分页缓冲区的后备链表列表。 从 Windows Vista 开始， <strong>LOOKASIDE_LIST_EX</strong>结构可以描述包含分页或非分页缓冲区的后备链表列表。 有关详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">Using 后备链表 Lists</a>。</p>
<p>在64位平台上，此结构必须为16字节对齐。</p>
<p>支持从 Windows 2000 开始。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>RTL_BITMAP</strong></td>
<td><p><strong>RTL_BITMAP</strong>结构是描述位图的不透明结构。</p>
<pre class="syntax"><code>typedef struct _RTL_BITMAP {
  // opaque
} RTL_BITMAP, *PRTL_BITMAP;</code></pre>
<p>不要直接访问此结构的成员。 直接依赖于成员位置或访问成员值的驱动程序可能不会与 Windows 操作系统的未来版本保持兼容。</p>
<p><strong>RTL_BITMAP</strong>结构充当任意长度的通用位图位图的标头。 驱动程序可以使用这样的位图来跟踪一组可重用项。 例如，文件系统可以使用位图来跟踪硬盘上已经分配了哪些群集和扇区来保存文件数据。</p>
<p>有关使用<strong>RTL_BITMAP</strong>结构的<strong>Rtl<em>Xxx</em></strong> 例程的列表，请参阅下面的另请参阅部分。 这些<strong>Rtl<em>Xxx</em></strong> 例程的调用方负责为<strong>RTL_BITMAP</strong>结构分配存储，为包含位图的缓冲区分配存储空间。 此缓冲区必须在内存中的四字节边界处开始，且长度必须为四个字节的倍数。 该位图从缓冲区的开头开始，但可以包含分配的缓冲区中容纳的任意数量的位数。</p>
<p>在将<strong>RTL_BITMAP</strong>结构作为<strong>RTL<em>Xxx</em></strong> 例程的参数提供之前，请调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitializebitmap" data-raw-source="[&lt;strong&gt;RtlInitializeBitMap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitializebitmap)"><strong>RtlInitializeBitMap</strong></a>例程来初始化该结构。 此例程的输入参数是指向缓冲区的指针，该缓冲区包含位图和位图的大小（以位为单位）。 <strong>RtlInitializeBitMap</strong>不会更改此缓冲区的内容。</p>
<p>如果调用方在分页内存中为<strong>RTL_BITMAP</strong>结构和位图分配存储空间，则调用方必须在 IRQL &lt;= APC_LEVEL 时运行，前提是它将指向此结构的指针作为参数传递给任意<strong>RTL<em>Xxx</em></strong> 例程"另请参阅" 部分中列出。 如果调用方从非分页内存（或等效于锁定的分页内存）分配存储，则调用方可以在调用<strong>Rtl<em>Xxx</em></strong> 例程时在任何 IRQL 上运行。</p>
<p>在 windows 2000 和更高版本的 Windows 中受支持。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p><strong>RTL_RUN_ONCE</strong>结构是一个不透明的结构，它存储一次初始化的信息。</p>
<p>驱动程序必须先调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceinitialize" data-raw-source="[&lt;strong&gt;RtlRunOnceInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceinitialize)"><strong>RtlRunOnceInitialize</strong></a>例程，然后再将其传递给任何其他<strong>RtlRunOnce<em>Xxx</em></strong> 例程，从而初始化此结构。</p>
<p>仅在 windows Vista 和更高版本的 Windows 操作系统上可用。</p>
<p>标头： Ntddk。 包括： Ntddk。</p></td>
</tr>
<tr class="odd">
<td><strong>SECURITY_SUBJECT_CONTEXT</strong></td>
<td><p><strong>SECURITY_SUBJECT_CONTEXT</strong>结构是一个不透明的结构，它表示发生特定操作的安全上下文。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="even">
<td><strong>SLIST_HEADER</strong></td>
<td><p><strong>SLIST_HEADER</strong>结构是一个不透明的结构，它充当排序的单向链接列表的标头。 有关详细信息，请参阅单个<a href="singly-and-doubly-linked-lists.md" data-raw-source="[Singly and Doubly Linked Lists](singly-and-doubly-linked-lists.md)">和双重链接列表</a>。</p>
<p>在64位平台上， <strong>SLIST_HEADER</strong>结构必须是16字节对齐的。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
<tr class="odd">
<td><strong>XSTATE_SAVE</strong></td>
<td><p><strong>XSTATE_SAVE</strong>结构是描述内核模式驱动程序保存和还原的扩展处理器状态信息的不透明结构。</p>
<pre class="syntax"><code>typedef struct _XSTATE_SAVE {
  ...  // opaque
} XSTATE_SAVE, *PXSTATE_SAVE;</code></pre>
<p>所有成员都不透明。</p>
<p>此结构由<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeSaveExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)"><strong>KeSaveExtendedProcessorState</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeRestoreExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)"><strong>KeRestoreExtendedProcessorState</strong></a>例程使用。</p>
<p>在 windows 7 和更高版本的 Windows 操作系统中受支持。</p>
<p>标头： Wdm .h。 Include： Wdm、Ntddk、Ntifs。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))  
[**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))  
[**ExAllocateFromLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromlookasidelistex)  
[**ExAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist)  
[**ExAllocateFromPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)  
[**ExAllocateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)  
[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)  
[**ExFreeToPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)  
[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)  
[**ExCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer)  
[**ExDeleteLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletelookasidelistex)  
[**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)  
[**ExDeleteTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer)  
[**ExFlushLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exflushlookasidelistex)  
[**ExFreeToLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetolookasidelistex)  
[**ExFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)  
[**ExInitializeLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)  
[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)  
[**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)  
[**ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedflushslist)  
[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist)  
[**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist)  
[**ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exquerydepthslist)  
[**ExReleaseFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545549(v=vs.85))  
[**ExReleaseFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545567(v=vs.85))  
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)  
[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))  
[*ExTimerCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_callback)  
[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)  
[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)  
[**IoCsqInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize)  
[**IoCsqInitializeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex)  
[**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)  
[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)  
[**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)  
[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)  
[**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)  
[**IoInitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem)  
[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)  
[**IoUninitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem)  
[**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))  
[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))  
[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))  
[**KeAcquireInterruptSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))  
[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)  
[**KeInitializeCallbackRecord**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)  
[**KeInitializeGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeguardedmutex)  
[**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)  
[**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)  
[**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)  
[**KeRestoreExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)  
[**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)  
[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)  
[**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)  
[**KeDeregisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckcallback)  
[**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)  
[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)  
[**KeRegisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback)  
[**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)  
[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)  
[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)  
[**KeReleaseInterruptSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinterruptspinlock)  
[**KeRestoreFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)  
[**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)  
[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)  
[*LookasideListAllocateEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-allocate_function_ex)  
[*LookasideListFreeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-free_function_ex)  
[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)  
[**PsGetCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)  
[**PsGetProcessCreateTimeQuadPart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)  
[**PsInitialSystemProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)  
[**PsIsSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psissystemthread)  
[**RtlRunOnceBeginInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunoncebegininitialize)  
[**RtlRunOnceComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunoncecomplete)  
[**RtlRunOnceExecuteOnce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceexecuteonce)  
[**RtlRunOnceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceinitialize)  
[*RunOnceInitialization*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-rtl_run_once_init_fn)  
[运行时保护](run-down-protection.md)  
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)  
[**SeAssignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seassignsecurity)  
[**SeAssignSecurityEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seassignsecurityex)  



