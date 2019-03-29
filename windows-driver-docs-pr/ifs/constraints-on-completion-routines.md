---
title: 完成例程的约束
description: 完成例程的约束
ms.assetid: 3873fd27-cfa8-414d-9437-c0789b20ff27
keywords:
- IRP 完成例程 WDK 文件系统，约束
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef0e4a1b84b672d7a5f0c21e90c8d7a75ba24ded
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564761"
---
# <a name="constraints-on-completion-routines"></a>完成例程的约束


## <span id="ddk_constraints_on_completion_routines_if"></span><span id="DDK_CONSTRAINTS_ON_COMPLETION_ROUTINES_IF"></span>


以下准则将简要介绍如何避免文件系统筛选器驱动程序完成例程中的常见编程错误。

### <a name="span-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL 相关约束

因为可以在 IRQL 调度调用完成例程\_级别，它们受到以下限制：

-   完成例程不能安全地调用，如要求较低的 IRQL，内核模式例程[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)或[ **ObQueryNameString** ](https://msdn.microsoft.com/library/windows/hardware/ff550990).

-   在完成例程中使用任何数据结构必须通过非分页缓冲池分配。

-   完成例程不能成为可分页。

-   完成例程无法获取互斥体或快速互斥锁资源。 但是，它们能够获取自旋锁。

### <a name="span-idcheckingthependingreturnedflagspanspan-idcheckingthependingreturnedflagspanspan-idcheckingthependingreturnedflagspanchecking-the-pendingreturned-flag"></a><span id="Checking_the_PendingReturned_Flag"></span><span id="checking_the_pendingreturned_flag"></span><span id="CHECKING_THE_PENDINGRETURNED_FLAG"></span>检查 PendingReturned 标志

-   除非完成例程向事件发出信号，则必须检查**Irp-&gt;PendingReturned**标志。 如果设置此标志，必须调用完成例程[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)将标记为正在等待 IRP。

-   如果完成例程向事件发出信号，则不应调用[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)。

### <a name="span-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>返回状态的约束

-   文件系统筛选器驱动程序完成例程必须返回任一状态\_成功或状态\_详细\_处理\_必需。 所有其他 NTSTATUS 值将重置为状态\_成功通过 I/O 管理器。

### <a name="span-idconstraintsonreturningstatusmoreprocessingrequiredspanspan-idconstraintsonreturningstatusmoreprocessingrequiredspanspan-idconstraintsonreturningstatusmoreprocessingrequiredspanconstraints-on-returning-statusmoreprocessingrequired"></a><span id="Constraints_on_Returning_STATUS_MORE_PROCESSING_REQUIRED"></span><span id="constraints_on_returning_status_more_processing_required"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS_MORE_PROCESSING_REQUIRED"></span>返回状态的约束\_更多\_处理\_必需

有三种情况时完成例程应返回状态\_更多\_处理\_必需：

-   当相应的调度例程正在等待事件完成例程的信号。 在这种情况下，务必返回状态\_更多\_处理\_必需以防止提前完成 IRP 之后完成例程返回, I/O 管理器。

-   当完成例程已发布到辅助队列 IRP 和相应的调度例程返回状态\_PENDING。 在这种情况下，务必要返回状态\_更多\_处理\_必需以防止提前完成 IRP 之后完成例程返回, I/O 管理器。

-   当相同的驱动程序通过调用创建 IRP [ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)或[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)。 驱动程序未从更高级别的驱动程序收到此 IRP，因为它可以安全地释放 IRP 中完成例程。 在调用[ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)，完成例程必须返回状态\_详细\_处理\_必需，指示没有进一步完成需要处理。

完成例程不能返回状态\_更多\_处理\_oplock 操作所需的。 机会锁操作不能被挂起 （发布到工作队列），和调度例程不能返回状态\_PENDING 它们。

### <a name="span-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>发布到工作队列的 Irp 的约束

-   如果完成例程将 Irp 发布到工作队列，它必须调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)之前发布每个 IRP 到辅助队列。 否则为无法取消排队，另一个驱动程序例程，完成并释放通过对调用之前系统 IRP **IoMarkIrpPending**发生，从而会导致崩溃。

 

 




