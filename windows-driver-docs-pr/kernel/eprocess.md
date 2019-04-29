---
title: Windows 内核不透明结构
description: Windows 内核不透明结构
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b22a03616aa0b43a2d46979510f19787c23d50a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361881"
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
<p>一些例程，如<a href="https://msdn.microsoft.com/library/windows/hardware/ff559939" data-raw-source="[&lt;strong&gt;PsGetProcessCreateTimeQuadPart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559939)"> <strong>PsGetProcessCreateTimeQuadPart</strong></a>，使用<strong>EPROCESS</strong>来识别要操作的进程。 驱动程序可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess" data-raw-source="[&lt;strong&gt;PsGetCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)"> <strong>PsGetCurrentProcess</strong> </a>例程，以获取指向过程的对象的当前进程，并可以使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong></a>例程，以获取与指定句柄关联的进程对象的指针。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559943" data-raw-source="[&lt;strong&gt;PsInitialSystemProcess&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559943)"> <strong>PsInitialSystemProcess</strong> </a>全局变量指向系统进程的进程对象。</p>
<p>请注意，将进程对象的对象管理器对象。 驱动程序应使用对象管理器例程如下所示<a href="https://msdn.microsoft.com/library/windows/hardware/ff558678" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558678)"> <strong>ObReferenceObject</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff557724" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557724)"> <strong>ObDereferenceObject</strong> </a>维护的对象引用计数。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p><strong>ETHREAD</strong>结构是可作为一个线程的线程对象的不透明结构。</p>
<p>一些例程，如<a href="https://msdn.microsoft.com/library/windows/hardware/ff559945" data-raw-source="[&lt;strong&gt;PsIsSystemThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559945)"> <strong>PsIsSystemThread</strong></a>，使用<strong>ETHREAD</strong>来标识要在上运行的线程。 驱动程序可以使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559936" data-raw-source="[&lt;strong&gt;PsGetCurrentThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559936)"> <strong>PsGetCurrentThread</strong> </a>例程，以获取指向该线程的当前线程对象，并可以使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong></a>例程，以获取与指定句柄关联的线程对象的指针。</p>
<p>请注意，线程对象的对象管理器对象。 驱动程序应使用对象管理器例程如下所示<a href="https://msdn.microsoft.com/library/windows/hardware/ff558678" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558678)"> <strong>ObReferenceObject</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff557724" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557724)"> <strong>ObDereferenceObject</strong> </a>维护的对象引用计数。</p>
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
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn265188" data-raw-source="[&lt;strong&gt;ExSetTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265188)"><strong>ExSetTimer</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn265180" data-raw-source="[&lt;strong&gt;ExCancelTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265180)"><strong>ExCancelTimer</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn265181" data-raw-source="[&lt;strong&gt;ExDeleteTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265181)"><strong>ExDeleteTimer</strong></a></li>
</ul>
<p><strong>EX_TIMER</strong>-由操作系统创建基于的计时器对象。 若要获取此类计时器对象，驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/dn265179" data-raw-source="[&lt;strong&gt;ExAllocateTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265179)"> <strong>ExAllocateTimer</strong> </a>例程。 当不再需要此对象时，该驱动程序负责通过调用删除对象<strong>ExDeleteTimer</strong>。</p>
<p>有关详细信息，请参阅<a href="exxxxtimer-routines-and-ex-timer-objects.md" data-raw-source="[Ex&lt;em&gt;Xxx&lt;/em&gt;Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md)">Ex<em>Xxx</em>计时器例程和 EX_TIMER 对象</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p>一个<strong>FAST_MUTEX</strong>结构是表示一个快速的互斥体的不透明的数据结构。</p>
<p>一个<strong>FAST_MUTEX</strong>结构初始化由<a href="https://msdn.microsoft.com/library/windows/hardware/ff545293" data-raw-source="[&lt;strong&gt;ExInitializeFastMutex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545293)"> <strong>ExInitializeFastMutex</strong> </a>例程。</p>
<p>有关快速互斥体的详细信息，请参阅<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">快速互斥锁和受保护的互斥体</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p><strong>IO_CSQ</strong>结构是用于指定驱动程序的取消安全 IRP 队列例程的不透明结构。 不能直接设置此结构的成员。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549054" data-raw-source="[&lt;strong&gt;IoCsqInitialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549054)"> <strong>IoCsqInitialize</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff549060" data-raw-source="[&lt;strong&gt;IoCsqInitializeEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549060)"> <strong>IoCsqInitializeEx</strong> </a>初始化此结构。</p>
<p>有关如何使用取消安全 IRP 队列的概述，请参阅<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">取消安全 IRP 队列</a>。</p>
<p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统上可用。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p><strong>IO_CSQ_IRP_CONTEXT</strong>结构是不透明的数据结构，用于指定的驱动程序的取消安全 IRP 队列中 IRP 的 IRP 上下文。 它用作通过键<a href="https://msdn.microsoft.com/library/windows/hardware/ff549066" data-raw-source="[&lt;strong&gt;IoCsqInsertIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549066)"> <strong>IoCsqInsertIrp</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff549067" data-raw-source="[&lt;strong&gt;IoCsqInsertIrpEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549067)"> <strong>IoCsqInsertIrpEx</strong></a>，并<a href="https://msdn.microsoft.com/library/windows/hardware/ff549070" data-raw-source="[&lt;strong&gt;IoCsqRemoveIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549070)"> <strong>IoCsqRemoveIrp</strong> </a>例程来标识特定 Irp 队列中的。</p>
<p>有关如何使用取消安全 IRP 队列的概述，请参阅<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">取消安全 IRP 队列</a>。</p>
<p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统上可用。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p><strong>IO_WORKITEM</strong>结构是描述系统工作线程的工作项的不透明结构。</p>
<p>驱动程序可以通过调用分配一个工作项<a href="https://msdn.microsoft.com/library/windows/hardware/ff548276" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548276)"> <strong>IoAllocateWorkItem</strong></a>。 或者，驱动程序可以分配其自己的缓冲区，然后调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549349" data-raw-source="[&lt;strong&gt;IoInitializeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549349)"> <strong>IoInitializeWorkItem</strong> </a>来初始化该缓冲区作为工作项。</p>
<p>分配的任何工作项<strong>IoAllocateWorkItem</strong>必须释放<a href="https://msdn.microsoft.com/library/windows/hardware/ff549133" data-raw-source="[&lt;strong&gt;IoFreeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549133)"> <strong>IoFreeWorkItem</strong></a>。 任何情况下将初始化的内存<strong>IoInitializeWorkItem</strong>必须通过未初始化<a href="https://msdn.microsoft.com/library/windows/hardware/ff550392" data-raw-source="[&lt;strong&gt;IoUninitializeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550392)"> <strong>IoUninitializeWorkItem</strong> </a>可释放之前。</p>
<p>有关工作项的详细信息，请参阅<a href="system-worker-threads.md" data-raw-source="[System Worker Threads](system-worker-threads.md)">系统工作线程数</a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_CALLBACK_RECORD</strong>结构是由不透明结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff553105" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553105)"> <strong>KeRegisterBugCheckCallback</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff551992" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551992)"> <strong>KeDeregisterBugCheckCallback</strong> </a>例程。</p>
<p><strong>KBUGCHECK_CALLBACK_RECORD</strong>结构用于由<a href="https://msdn.microsoft.com/library/windows/hardware/ff553110" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553110)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff552003" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552003)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>例程。</p>
<p>必须在常驻内存中，如非分页缓冲池分配结构。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552109" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552109)"> <strong>KeInitializeCallbackRecord</strong> </a>例程使用它之前初始化结构。</p>
<p>标头：Ntddk.h。 包括：Ntddk.h。</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>结构是由不透明结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff553110" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553110)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff552003" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552003)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>例程。</p>
<p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>结构用于由<a href="https://msdn.microsoft.com/library/windows/hardware/ff553110" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553110)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff552003" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552003)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>例程。</p>
<p>必须在常驻内存中，如非分页缓冲池分配结构。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552109" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552109)"> <strong>KeInitializeCallbackRecord</strong> </a>例程使用它之前初始化结构。</p>
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
<td><p><strong>KFLOATING_SAVE</strong>结构是一个不透明结构描述的浮点状态<a href="https://msdn.microsoft.com/library/windows/hardware/ff553243" data-raw-source="[&lt;strong&gt;KeSaveFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553243)"> <strong>KeSaveFloatingPointState</strong> </a>保存的例程。</p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553185" data-raw-source="[&lt;strong&gt;KeRestoreFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553185)"> <strong>KeRestoreFloatingPointState</strong> </a>要还原的浮点状态。</p>
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
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548378" data-raw-source="[&lt;strong&gt;IoConnectInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548378)"><strong>IoConnectInterruptEx</strong> </a>提供一个指针指向<strong>KINTERRUPT</strong>中断时该驱动程序注册的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff547958" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547958)"> <em>InterruptService</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff547940" data-raw-source="[&lt;em&gt;InterruptMessageService&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547940)"> <em>InterruptMessageService</em> </a>例程。 驱动程序使用此指针时获取或释放中断的中断自旋锁。 驱动程序还使用此指针时注销<em>InterruptService</em>例程。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p><strong>KLOCK_QUEUE_HANDLE</strong>结构是描述排队的旋转锁的不透明结构。 驱动程序分配了<strong>KLOCK_QUEUE_HANDLE</strong>结构，并将其传递给<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff551908" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551908)"> <strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong> </a>获取排队的自旋锁。 这些例程初始化该结构以表示排队的自旋锁。 该驱动程序将向此结构传递<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff553137" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553137)"> <strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong> </a>当释放自旋锁。</p>
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
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545301" data-raw-source="[&lt;strong&gt;ExInitializeNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545301)"> <strong>ExInitializeNPagedLookasideList</strong> </a>初始化后备链列表。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544388" data-raw-source="[&lt;strong&gt;ExAllocateFromNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544388)"> <strong>ExAllocateFromNPagedLookasideList</strong> </a>来分配缓冲区从列表中，并且<a href="https://msdn.microsoft.com/library/windows/hardware/ff544601" data-raw-source="[&lt;strong&gt;ExFreeToNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544601)"> <strong>ExFreeToNPagedLookasideList</strong> </a>返回到列表的缓冲区。</p>
<p>驱动程序必须始终显式地释放它们在卸载之前创建的任何后备链列表。 严重的编程错误，否则它。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544566" data-raw-source="[&lt;strong&gt;ExDeleteNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544566)"> <strong>ExDeleteNPagedLookasideList</strong> </a>来释放列表。</p>
<p>驱动程序还可以为页面缓冲池使用后备链列表。 从 Windows 2000 <strong>PAGED_LOOKASIDE_LIST</strong>结构描述包含分页的缓冲区的后备链列表。 从 Windows Vista 开始<strong>LOOKASIDE_LIST_EX</strong>结构可以描述包含分页或非分页缓冲区的后备链列表。 有关详细信息，请参阅<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">使用后备链列表</a>。</p>
<p>在 64 位平台上，此结构必须是 16 字节对齐。</p>
<p>支持从 Windows 2000 开始。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong>是指定的句柄的对象类型的不透明结构。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong></a>。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>PAGED_LOOKASIDE_LIST</strong>结构是描述固定大小缓冲区从页面缓冲池分配的后备链列表的不透明结构。 系统将创建新的项，并销毁根据列表上未使用的条目。 对于固定大小的缓冲区，使用后备链列表是快于直接分配的内存。</p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545309" data-raw-source="[&lt;strong&gt;ExInitializePagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545309)"> <strong>ExInitializePagedLookasideList</strong> </a>初始化后备链列表。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544393" data-raw-source="[&lt;strong&gt;ExAllocateFromPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544393)"> <strong>ExAllocateFromPagedLookasideList</strong> </a>来分配缓冲区从列表中，并且<a href="https://msdn.microsoft.com/library/windows/hardware/ff544605" data-raw-source="[&lt;strong&gt;ExFreeToPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544605)"> <strong>ExFreeToPagedLookasideList</strong> </a>返回到列表的缓冲区。</p>
<p>驱动程序必须始终显式地释放它们在卸载之前创建的任何后备链列表。 严重的编程错误，否则它。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544570" data-raw-source="[&lt;strong&gt;ExDeletePagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544570)"> <strong>ExDeletePagedLookasideList</strong> </a>来释放列表。</p>
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
<p>提供之前<strong>RTL_BITMAP</strong>作为参数的结构<strong>Rtl<em>Xxx</em></strong> 例程，调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff561925" data-raw-source="[&lt;strong&gt;RtlInitializeBitMap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561925)"> <strong>RtlInitializeBitMap</strong></a>例程初始化结构。 此例程的输入的参数是位图的指向包含位图，并以位为单位的大小的缓冲区的指针。 <strong>RtlInitializeBitMap</strong>不会更改此缓冲区的内容。</p>
<p>如果调用方分配的存储<strong>RTL_BITMAP</strong>结构和分页内存中的位图，调用方必须在 IRQL 运行&lt;= APC_LEVEL 时它将指针传递给此结构作为参数任一<strong>Rtl<em>Xxx</em></strong> 另请参阅部分中列出的例程。 如果调用方分配存储，从非分页内存 （或，也可以说锁定的分页内存），可以运行的任何 irql 的调用方调用时<strong>Rtl<em>Xxx</em></strong> 例程。</p>
<p>支持在 Windows 2000 和更高版本的 Windows。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p><strong>RTL_RUN_ONCE</strong>结构是将存储一次性初始化的信息的不透明结构。</p>
<p>驱动程序必须通过调用初始化此结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff562767" data-raw-source="[&lt;strong&gt;RtlRunOnceInitialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562767)"> <strong>RtlRunOnceInitialize</strong> </a>然后再将它传递到任何其他例程<strong>RtlRunOnce<em>Xxx</em></strong> 例程。</p>
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
<p>此结构可供<a href="https://msdn.microsoft.com/library/windows/hardware/ff553238" data-raw-source="[&lt;strong&gt;KeSaveExtendedProcessorState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553238)"> <strong>KeSaveExtendedProcessorState</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff553182" data-raw-source="[&lt;strong&gt;KeRestoreExtendedProcessorState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553182)"> <strong>KeRestoreExtendedProcessorState</strong> </a>例程。</p>
<p>Windows 7 和更高版本的 Windows 操作系统支持。</p>
<p>标头：Wdm.h。 包括：Wdm.h 中 Ntddk.h，Ntifs.h。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff544337)  
[**ExAcquireFastMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff544340)  
[**ExAllocateFromLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544381)  
[**ExAllocateFromNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544388)  
[**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)  
[**ExAllocateTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265179)  
[**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)  
[**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)  
[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)  
[**ExCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265180)  
[**ExDeleteLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544563)  
[**ExDeleteNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544566)  
[**ExDeleteTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265181)  
[**ExFlushLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544587)  
[**ExFreeToLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544597)  
[**ExFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544601)  
[**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)  
[**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)  
[**ExInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff545321)  
[**ExInterlockedFlushSList**](https://msdn.microsoft.com/library/windows/hardware/ff545379)  
[**ExInterlockedPopEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545414)  
[**ExInterlockedPushEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545422)  
[**ExQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff545502)  
[**ExReleaseFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545549)  
[**ExReleaseFastMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff545567)  
[**ExSetTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265188)  
[**ExTryToAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545647)  
[*ExTimerCallback*](https://msdn.microsoft.com/library/windows/hardware/dn265190)  
[**IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)  
[**IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378)  
[**IoCsqInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff549054)  
[**IoCsqInitializeEx**](https://msdn.microsoft.com/library/windows/hardware/ff549060)  
[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)  
[**IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067)  
[**IoCsqRemoveIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549070)  
[**IoDisconnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff549093)  
[**IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)  
[**IoInitializeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549349)  
[**IoRequestDpc**](https://msdn.microsoft.com/library/windows/hardware/ff549657)  
[**IoUninitializeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff550392)  
[**KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)  
[**KeAcquireGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff551894)  
[**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551908)  
[**KeAcquireInterruptSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551914)  
[**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)  
[**KeInitializeCallbackRecord**](https://msdn.microsoft.com/library/windows/hardware/ff552109)  
[**KeInitializeGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff552144)  
[**KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)  
[**KeInitializeTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff552173)  
[**KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)  
[**KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)  
[**KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)  
[**KeSetTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553286)  
[**KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)  
[**KeDeregisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff551992)  
[**KeDeregisterBugCheckReasonCallback**](https://msdn.microsoft.com/library/windows/hardware/ff552003)  
[**KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)  
[**KeRegisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553105)  
[**KeRegisterBugCheckReasonCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553110)  
[**KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)  
[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)  
[**KeReleaseInterruptSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553139)  
[**KeRestoreFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553185)  
[**KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)  
[**KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)  
[*LookasideListAllocateEx*](https://msdn.microsoft.com/library/windows/hardware/ff554322)  
[*LookasideListFreeEx*](https://msdn.microsoft.com/library/windows/hardware/ff554324)  
[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)  
[**PsGetCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)  
[**PsGetProcessCreateTimeQuadPart**](https://msdn.microsoft.com/library/windows/hardware/ff559939)  
[**PsInitialSystemProcess**](https://msdn.microsoft.com/library/windows/hardware/ff559943)  
[**PsIsSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559945)  
[**RtlRunOnceBeginInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562759)  
[**RtlRunOnceComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562763)  
[**RtlRunOnceExecuteOnce**](https://msdn.microsoft.com/library/windows/hardware/ff562765)  
[**RtlRunOnceInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562767)  
[*RunOnceInitialization*](https://msdn.microsoft.com/library/windows/hardware/ff563635)  
[Run-Down 保护](run-down-protection.md)  
[**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)  
[**SeAssignSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff563676)  
[**SeAssignSecurityEx**](https://msdn.microsoft.com/library/windows/hardware/ff563679)  



