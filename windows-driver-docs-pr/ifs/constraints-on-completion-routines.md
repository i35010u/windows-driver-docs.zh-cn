---
title: 完成例程的约束
description: 完成例程的约束
ms.assetid: 3873fd27-cfa8-414d-9437-c0789b20ff27
keywords:
- IRP 完成例程 WDK 文件系统，约束
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ed54a0c334ec16d2d0bae56c6f7b9035289d7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841456"
---
# <a name="constraints-on-completion-routines"></a>完成例程的约束


## <span id="ddk_constraints_on_completion_routines_if"></span><span id="DDK_CONSTRAINTS_ON_COMPLETION_ROUTINES_IF"></span>


以下准则简要介绍了如何避免文件系统筛选器驱动程序完成例程中出现常见的编程错误。

### <a name="span-idirql-related_constraintsspanspan-idirql-related_constraintsspanspan-idirql-related_constraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL 相关的约束

由于可以在 IRQL 调度\_级别调用完成例程，因此它们服从以下限制：

-   完成例程无法安全调用需要较低 IRQL 的内核模式例程，如[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)或[**ObQueryNameString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-obquerynamestring)。

-   完成例程中使用的所有数据结构必须从非分页池进行分配。

-   完成例程无法进行分页。

-   完成例程无法获取资源、互斥体或快速 mutex。 但是，它们可以获取自旋锁。

### <a name="span-idchecking_the_pendingreturned_flagspanspan-idchecking_the_pendingreturned_flagspanspan-idchecking_the_pendingreturned_flagspanchecking-the-pendingreturned-flag"></a><span id="Checking_the_PendingReturned_Flag"></span><span id="checking_the_pendingreturned_flag"></span><span id="CHECKING_THE_PENDINGRETURNED_FLAG"></span>检查 PendingReturned 标志

-   除非完成例程向事件发出信号，否则必须检查**Irp&gt;PendingReturned**标志。 如果设置了此标志，则完成例程必须调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，将 IRP 标记为挂起。

-   如果完成例程发出事件信号，则不应调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)。

### <a name="span-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>返回状态的约束

-   文件系统筛选器驱动程序完成例程必须返回状态\_"成功" 或 "状态"，\_需要\_更多\_处理。 所有其他的 NTSTATUS 值都将重置为 i/o 管理器成功\_状态。

### <a name="span-idconstraints_on_returning_status_more_processing_requiredspanspan-idconstraints_on_returning_status_more_processing_requiredspanspan-idconstraints_on_returning_status_more_processing_requiredspanconstraints-on-returning-status_more_processing_required"></a><span id="Constraints_on_Returning_STATUS_MORE_PROCESSING_REQUIRED"></span><span id="constraints_on_returning_status_more_processing_required"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS_MORE_PROCESSING_REQUIRED"></span>有关返回状态的约束\_\_需要更多的\_处理

在以下三种情况下，完成例程应返回状态\_更多\_处理\_必需：

-   当相应的调度例程等待由完成例程发出的事件时。 在这种情况下，请务必返回状态\_更多\_处理\_需要此方法，以防止 i/o 管理器在完成例程返回后提前完成 IRP。

-   完成例程将 IRP 发送到辅助角色队列后，相应的调度例程返回状态\_"挂起"。 在这种情况下，请务必返回状态\_更多\_处理\_需要此方法，以防止 i/o 管理器在完成例程返回后提前完成 IRP。

-   同一驱动程序通过调用[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)或[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)创建 IRP。 由于驱动程序没有从更高级别的驱动程序接收到此 IRP，因此它可以安全地在完成例程中释放 IRP。 在调用[**IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)之后，完成例程必须返回状态\_更多\_处理\_需要指示不再需要完成处理。

完成例程无法返回状态\_需要执行 oplock 操作所需的\_处理\_。 Oplock 操作不能挂起（发布到辅助角色队列），调度例程无法返回状态\_挂起。

### <a name="span-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>将 Irp 发送到工作队列的约束

-   如果完成例程将 Irp 发送到工作队列，则必须先调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，然后才能将每个 irp 发送到工作队列。 否则，IRP 可以取消排队，由其他驱动程序例程完成，并在调用**也**之前由系统释放，从而导致崩溃。

 

 




