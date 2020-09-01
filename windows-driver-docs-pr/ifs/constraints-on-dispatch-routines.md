---
title: 调度例程的约束
description: 调度例程的约束
ms.assetid: 5b2acaea-1f66-4285-9a36-5ab0f440f6b4
keywords:
- IRP 调度例程 WDK 文件系统，约束
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38d21976872d69e643bae2633f76ca77ec2082ae
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065114"
---
# <a name="constraints-on-dispatch-routines"></a>调度例程的约束


## <span id="ddk_constraints_on_dispatch_routines_if"></span><span id="DDK_CONSTRAINTS_ON_DISPATCH_ROUTINES_IF"></span>


以下准则简要介绍了如何避免在文件系统筛选器驱动程序的调度例程中出现常见的编程错误。

### <a name="span-idirql-related_constraintsspanspan-idirql-related_constraintsspanspan-idirql-related_constraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL 相关的约束

注意：有关在分页 i/o 中使用哪些类型的 Irp 的信息，请参阅 [调度例程 IRQL 和线程上下文](dispatch-routine-irql-and-thread-context.md)。

-   分页 i/o 路径中的调度例程绝不应在 APC 级别以上的任何 IRQL 上调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) \_ 。 如果调度例程引发 IRQL，则必须在调用 **IoCallDriver**之前将其降低。

-   分页路径中的调度例程（如读取和写入）无法安全调用任何需要调用方在 IRQL 被动级别运行的内核模式例程 \_ 。

-   页面文件 i/o 路径中的调度例程不能安全地调用任何要求调用方在 IRQL 调度级别运行的内核模式例程 &lt; \_ 。

-   不在分页 i/o 路径中的调度例程绝不应在被动级别以上[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的任何 IRQL 上调用 IoCallDriver \_ 。 如果调度例程引发 IRQL，则必须在调用 **IoCallDriver**之前将其降低。

### <a name="span-idconstraints_on_processing_irpsspanspan-idconstraints_on_processing_irpsspanspan-idconstraints_on_processing_irpsspanconstraints-on-processing-irps"></a><span id="Constraints_on_Processing_IRPs"></span><span id="constraints_on_processing_irps"></span><span id="CONSTRAINTS_ON_PROCESSING_IRPS"></span>处理 Irp 的约束

-   如果 IRP 参数包含任何用户空间地址，则必须在使用之前对其进行验证。 有关详细信息，请参阅 [缓冲 i/o 中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-buffered-i-o)。

-   此外，如果 IRP 包含从32位平台发送到64位平台的 IOCTL 或 FSCTL 缓冲区，则可能需要 thunked 缓冲区内容。 有关详细信息，请参阅 [64 位驱动程序中的支持32位 i/o](../kernel/supporting-32-bit-i-o-in-your-64-bit-driver.md)。

-   与文件系统不同，文件系统筛选器驱动程序绝不应调用 [**FsRtlEnterFileSystem**](./fsrtlenterfilesystem.md) 或 [**FsRtlExitFileSystem**](./fsrtlexitfilesystem.md) ，除非调用 [**ExAcquireFastMutexUnsafe**](/previous-versions/windows/hardware/drivers/ff544340(v=vs.85)) 或 [**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))。 **FsRtlEnterFileSystem** 和 **FsRtlExitFileSystem** 禁用正常内核 apc，这是大多数文件系统所需的。

### <a name="span-idconstraints_on_completing_irpsspanspan-idconstraints_on_completing_irpsspanspan-idconstraints_on_completing_irpsspanconstraints-on-completing-irps"></a><span id="Constraints_on_Completing_IRPs"></span><span id="constraints_on_completing_irps"></span><span id="CONSTRAINTS_ON_COMPLETING_IRPS"></span>完成 Irp 的约束

-   完成 Irp 后，文件系统筛选器驱动程序应仅使用成功和错误状态值。

-   尽管状态 \_ "挂起" 是成功的 NTSTATUS 值，但它是用于完成状态为 "挂起" 的 IRP 的编程错误 \_ 。

-   调度例程调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)后，IRP 指针将不再有效，且不能安全地取消引用。

### <a name="span-idconstraints_on_setting_a_completion_routinespanspan-idconstraints_on_setting_a_completion_routinespanspan-idconstraints_on_setting_a_completion_routinespanconstraints-on-setting-a-completion-routine"></a><span id="Constraints_on_Setting_a_Completion_Routine"></span><span id="constraints_on_setting_a_completion_routine"></span><span id="CONSTRAINTS_ON_SETTING_A_COMPLETION_ROUTINE"></span>设置完成例程的约束

注意：有关设置完成例程的信息，请参阅 [使用完成例程](using-irp-completion-routines.md)。

-   当调度例程调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)时，它可以选择将 *上下文* 指针传递到结构，以便完成例程在处理给定的 IRP 时使用。 此结构必须从非分页池分配，因为完成例程可以被称为 IRQL 调度 \_ 级别。

-   如果派单例程设置的完成例程可能返回 \_ 需要更多 \_ 的处理状态 \_ ，则必须执行以下操作之一来阻止 i/o 管理器提前完成 IRP：
    -   将 IRP 标记为 "挂起"，调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)，并返回 "挂起" 状态 \_ 。
    -   调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 以等待完成例程执行，然后调用 [**IOCOMPLETEREQUEST**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 IRP。

### <a name="span-idconstraints_on_passing_irps_downspanspan-idconstraints_on_passing_irps_downspanspan-idconstraints_on_passing_irps_downspanconstraints-on-passing-irps-down"></a><span id="Constraints_on_Passing_IRPs_Down"></span><span id="constraints_on_passing_irps_down"></span><span id="CONSTRAINTS_ON_PASSING_IRPS_DOWN"></span>将 Irp 向下传递的约束

-   在调度例程调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)后，IRP 指针不再有效且不能安全地取消引用，除非调度例程等待完成例程通知它已被调用。

-   从文件系统筛选器驱动程序调用 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 的编程错误。  (**PoCallDriver** 用于将 IRP \_ MJ \_ 电源请求传递给较低级别的驱动程序。 文件系统筛选器驱动程序绝不会接收 IRP \_ MJ \_ POWER 请求。 ) 

### <a name="span-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>返回状态的约束

-   除非在完成 IRP 时，未设置完成例程的调度例程应始终返回 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)返回的 NTSTATUS 值。 除非此值处于 \_ "挂起" 状态，否则它必须与完成 irp 的驱动程序设置的 IoStatus 的值匹配** &gt; 。**

-   当 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 返回状态 \_ "挂起" 时，调度例程还应返回 \_ "挂起" 状态，除非它等待完成例程向事件发出信号。

-   将 IRP 发送到辅助角色队列以便以后处理时，调度例程应将 IRP 标记为 "正在挂起" 并返回 "挂起" 状态 \_ 。

-   将 IRP 设置为将 IRP 发送到辅助角色队列以便以后处理时，调度例程应将 IRP 标记为 "正在挂起" 并返回 "挂起" 状态 \_ 。

-   标记 IRP "挂起" 的调度例程必须返回 " \_ 挂起" 状态。

-   不能暂停 Oplock 操作 (将其发布到工作队列) ，调度例程无法返回 \_ 其挂起状态。

### <a name="span-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>将 Irp 发送到工作队列的约束

-   如果调度例程将 Irp 发送到工作队列，则必须先调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) ，然后才能将每个 irp 发送到工作队列。 否则，IRP 可以取消排队，由其他驱动程序例程完成，并在调用 **也** 之前由系统释放，从而导致崩溃。

 

