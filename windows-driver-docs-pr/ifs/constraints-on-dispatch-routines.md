---
title: 调度例程的约束
description: 调度例程的约束
ms.assetid: 5b2acaea-1f66-4285-9a36-5ab0f440f6b4
keywords:
- IRP 调度例程 WDK 文件系统，约束
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9de130d7491ec0957f196c9e63e0076649e918d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561883"
---
# <a name="constraints-on-dispatch-routines"></a>调度例程的约束


## <span id="ddk_constraints_on_dispatch_routines_if"></span><span id="DDK_CONSTRAINTS_ON_DISPATCH_ROUTINES_IF"></span>


以下准则将简要介绍如何避免文件系统筛选器驱动程序的调度例程中的常见编程错误。

### <a name="span-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL 相关约束

注意：有关哪些类型的 Irp 使用分页 I/O 中的信息，请参阅[调度例程 IRQL 和线程上下文](dispatch-routine-irql-and-thread-context.md)。

-   分页 I/O 路径中的调度例程应永远不会调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)在上面 APC 的任何 IRQL\_级别。 如果调度例程引发的 IRQL，它必须将它降级，然后再调**IoCallDriver**。

-   调度例程中的分页路径，例如读取和写入，不能安全地调用要求调用方在被动 IRQL 运行任意内核模式例程\_级别。

-   分页文件 I/O 路径中的调度例程不能安全地调用要求调用方在 IRQL 运行任意内核模式例程&lt;调度\_级别。

-   不在分页 I/O 路径中的调度例程应永远不会调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)在被动上方的任何 IRQL\_级别。 如果调度例程引发的 IRQL，它必须将它降级，然后再调**IoCallDriver**。

### <a name="span-idconstraintsonprocessingirpsspanspan-idconstraintsonprocessingirpsspanspan-idconstraintsonprocessingirpsspanconstraints-on-processing-irps"></a><span id="Constraints_on_Processing_IRPs"></span><span id="constraints_on_processing_irps"></span><span id="CONSTRAINTS_ON_PROCESSING_IRPS"></span>处理 Irp 的约束

-   如果 IRP 参数中包含的所有用户空间地址，必须在使用之前验证这些。 有关详细信息，请参阅[缓冲 I/O 中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544293)。

-   此外，如果 IRP 包含已从 32 位平台发送到 64 位平台的 IOCTL 或 FSCTL 缓冲区，缓冲区内容可能需要将 thunked。 有关详细信息，请参阅[在 64 位驱动程序中支持 32 位 I/O](https://msdn.microsoft.com/library/windows/hardware/ff563897)。

-   文件系统筛选器驱动程序应永远不会调用与文件系统不同[ **FsRtlEnterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff545900)或[ **FsRtlExitFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff545908)除外然后再调用[ **ExAcquireFastMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff544340)或[ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)。 **FsRtlEnterFileSystem**并**FsRtlExitFileSystem**禁用正常内核 Apc，所需的大多数文件系统。

### <a name="span-idconstraintsoncompletingirpsspanspan-idconstraintsoncompletingirpsspanspan-idconstraintsoncompletingirpsspanconstraints-on-completing-irps"></a><span id="Constraints_on_Completing_IRPs"></span><span id="constraints_on_completing_irps"></span><span id="CONSTRAINTS_ON_COMPLETING_IRPS"></span>完成 Irp 的约束

-   完成后 Irp，文件系统筛选器驱动程序应使用唯一的成功和错误状态的值。

-   尽管状态\_PENDING 是成功 NTSTATUS 值，而是编程错误才能完成，状态 IRP\_PENDING。

-   调度例程调用后[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)，IRP 指针不再有效，不能安全地取消引用。

### <a name="span-idconstraintsonsettingacompletionroutinespanspan-idconstraintsonsettingacompletionroutinespanspan-idconstraintsonsettingacompletionroutinespanconstraints-on-setting-a-completion-routine"></a><span id="Constraints_on_Setting_a_Completion_Routine"></span><span id="constraints_on_setting_a_completion_routine"></span><span id="CONSTRAINTS_ON_SETTING_A_COMPLETION_ROUTINE"></span>设置完成例程的约束

注意：有关设置完成例程的信息，请参阅[使用完成例程](using-irp-completion-routines.md)。

-   当调用的调度例程[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)，可以选择性地传递*上下文*完成例程处理时要使用的结构的指针给定的 IRP。 此结构必须分配从非分页缓冲池，因为完成例程可调用的 IRQL 调度\_级别。

-   如果调度例程设置可能会返回状态完成例程\_更多\_处理\_必需的它必须执行下列任一操作，阻止过早地完成 IRP I/O 管理器：
    -   将标记挂起调用 IRP [ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)，并返回状态\_PENDING。
    -   调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)若要等待执行完成例程，然后调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成IRP。

### <a name="span-idconstraintsonpassingirpsdownspanspan-idconstraintsonpassingirpsdownspanspan-idconstraintsonpassingirpsdownspanconstraints-on-passing-irps-down"></a><span id="Constraints_on_Passing_IRPs_Down"></span><span id="constraints_on_passing_irps_down"></span><span id="CONSTRAINTS_ON_PASSING_IRPS_DOWN"></span>向下传递 Irp 的约束

-   调度例程调用后[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)，IRP 指针将不再有效，并且不能安全地取消引用，除非调度例程等待完成例程来表示它已已调用。

-   它是编程错误调用[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)从文件系统筛选器驱动程序。 (**PoCallDriver**用于传递 IRP\_MJ\_电源较低级驱动程序的请求。 文件系统筛选器驱动程序永远不会接收 IRP\_MJ\_电源请求。)

### <a name="span-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>返回状态的约束

-   但不会设置完成例程的调度例程完成后 IRP，应始终返回返回的 NTSTATUS 值[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。 除非此值为状态\_挂起状态，它必须匹配的值**Irp-&gt;IoStatus.Status**完成 IRP 驱动程序设置。

-   当[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)返回状态\_挂起、 调度例程还会返回状态\_PENDING，除非它等待完成例程来使事件终止。

-   调度例程时发布到工作队列中进行更高版本处理 IRP，应将挂起的 IRP 标记并返回状态\_PENDING。

-   调度例程时设置完成例程可能会发布到工作队列中进行更高版本处理 IRP，应将挂起的 IRP 标记并返回状态\_PENDING。

-   将标记挂起的 IRP 的调度例程必须返回状态\_PENDING。

-   机会锁操作不能被挂起 （发布到工作队列），和调度例程不能返回状态\_PENDING 它们。

### <a name="span-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>发布到工作队列的 Irp 的约束

-   如果调度例程将 Irp 发布到工作队列，它必须调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)之前发布每个 IRP 到辅助队列。 否则为无法取消排队，另一个驱动程序例程，完成并释放通过对调用之前系统 IRP **IoMarkIrpPending**发生，从而会导致崩溃。

 

 




