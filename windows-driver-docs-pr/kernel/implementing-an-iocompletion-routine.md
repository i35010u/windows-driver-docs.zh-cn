---
title: 实现 IoCompletion 例程
description: 实现 IoCompletion 例程
ms.assetid: 669860b1-5e85-4b28-a9b1-1ccf8c689b7a
keywords:
- IoCompletion 例程
- IoCompleteRequest 例程
- 优先级提升 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a38ec71556eac99cddf9ca99df5d2686e7785fca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365818"
---
# <a name="implementing-an-iocompletion-routine"></a>实现 IoCompletion 例程





在进入时， [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程接收*上下文*指针。 当调用的调度例程[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)，它可以提供*上下文*指针。 此指针可以引用任何驱动程序确定上下文信息*IoCompletion*例程需要处理 IRP。 请注意，上下文区域不能为可分页因为*IoCompletion*例程可以调用在 IRQL = 调度\_级别。

**请考虑以下 IoCompletion 例程的实现准则：**

-   *IoCompletion*例程可以检查 IRP [I/O 状态块](i-o-status-blocks.md)以确定 I/O 操作的结果。

-   如果由调度例程，并使用分配输入的 IRP [ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)或[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)， *IoCompletion*例程必须调用[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)释放该 IRP，最好是在完成原始 IRP 之前。

    -   *IoCompletion*例程必须释放每个 IRP 的资源分配给驱动程序分配 IRP，最好是之前释放相应 IRP 的调度例程。

        例如，如果调度例程分配与 MDL [ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)并调用[ **IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)为它分配的部分传输 IRP *IoCompletion*例程必须释放与 MDL [ **IoFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)。 如果它分配资源来维护有关原始 IRP 的状态，它必须释放这些资源，最好是调用之前[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与原始的 IRP 和绝对它将返回之前控件。

        一般情况下，释放或完成 IRP 之前, *IoCompletion*例程应释放分配的调度例程任何 IRP 每个资源。 否则，该驱动程序必须维护状态有关的资源之前释放其*IoCompletion*例程完成原始请求将返回控制。

    -   如果*IoCompletion*例程无法完成状态与原始 IRP\_成功后，它必须在原始 IRP 到导致驱动程序分配 IRP 中返回的值中设置 I/O 状态块*IoCompletion*例程，以使原始请求失败。

    -   如果*IoCompletion*例程将完成状态为原始请求\_挂起状态，它必须调用[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)与原始的 IRP在调用之前**IoCompleteRequest**。

    -   如果*IoCompletion*例程时不能与错误状态原始 IRP\_*XXX*，它可以[记录错误](logging-errors.md)。 但是，它是基础的设备驱动程序，以记录所有的设备 I/O 错误的发生，这样的责任*IoCompletion*例程通常不会记录错误。

    -   当*IoCompletion*例程已处理和释放驱动程序分配 IRP，该例程必须返回具有状态控件\_详细\_处理\_必需。

        返回状态\_更多\_处理\_需*IoCompletion*例程防止驱动程序分配和释放 IRP 的处理的 I/O 管理器完成。 第二次调用**IoCompleteRequest**导致 I/O 管理器继续调用 IRP 的完成例程，从上面的例程的返回状态为完成例程\_详细\_处理\_必需。

-   如果*IoCompletion*例程重用传入 IRP 发送一个或多个请求，以降低驱动程序，或如果常规重试失败的操作，它应更新任何上下文*IoCompletion*例程维护有关每个重复使用或的 IRP 的重试。 然后它可以设置下一步低驱动程序的 I/O 堆栈位置再次调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)具有其自己的入口点和调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP 的。

    -   *IoCompletion*不应调用例程[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)在每个重复使用或的 IRP 的重试。

        调度例程已标记为正在等待原始 IRP。 直到链中的所有驱动程序完成与原始 IRP **IoCompleteRequest**，它将保持挂起。

    -   重试请求前*IoCompletion*例程应重置状态的 I/O 状态块\_成功**状态**对于该值为零**信息**，可能需要括在保存返回的错误信息。

        每次重试*IoCompletion*例程通常递减的重试计数集调度例程。 通常情况下， *IoCompletion*例程必须调用**IoCompleteRequest**失败 IRP 时一定数量有限的重试已失败。

    -   *IoCompletion*例程必须返回状态\_详细\_处理\_后它会调用所需[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)并[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)与 IRP 正被重复使用，或者重试。

        返回状态\_更多\_处理\_需*IoCompletion*例程防止 I/O 管理器完成处理的重复使用或重试 IRP。

    -   如果*IoCompletion*例程无法完成状态与原始 IRP\_成功后，它必须使 I/O 状态块所返回的较低的驱动程序会导致在重用或重试操作*IoCompletion*例程失败 IRP。

    -   如果*IoCompletion*例程将完成状态为原始请求\_挂起状态，它必须调用**IoMarkIrpPending**与原始 IRP 调用之前**IoCompleteRequest**。
    -   如果*IoCompletion*例程时不能与错误状态原始 IRP\_*XXX*，它可以[记录错误](logging-errors.md)。 但是，它是基础的设备驱动程序，以记录所有的设备 I/O 错误的发生，这样的责任*IoCompletion*例程通常不会记录错误。

-   设置任何驱动程序*IoCompletion* IRP 到较低的驱动程序应检查例程中 IRP，然后传递**IRP-&gt;PendingReturned**标志中*IoCompletion*例程。 如果设置了标志， *IoCompletion*例程必须调用**IoMarkIrpPending**与 IRP。 但请注意，将 IRP 下传递，然后等待事件的驱动程序应将挂起的 IRP 标记。 相反，其*IoCompletion*例程应发出事件信号并返回状态\_详细\_处理\_必需。

-   *IoCompletion*例程必须释放任何资源用于处理原始 IRP，最好是之前分配的调度例程*IoCompletion*例程调用**IoCompleteRequest**与原始的 IRP 和绝对之前*IoCompletion*例程将返回完成原始 IRP 控件。

如果任何更高级别的驱动程序已设置其*IoCompletion*中原始 IRP，该驱动程序的日常*IoCompletion*例程不调用直到*IoCompletion*例程较低级别的所有驱动程序调用了。

### <a name="supplying-a-priority-boost-in-calls-to-iocompleterequest"></a>提供对 IoCompleteRequest 的调用中的优先级提升

如果最低级别的设备驱动程序可以完成其调度例程中的 IRP，则会调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与*PriorityBoost* IO 的\_没有\_增量。 需要未运行时优先级增加，因为该驱动程序可以假定，原始请求者不会等待其 I/O 操作完成。

否则，最低级别驱动程序将提供提升请求方的运行时优先级，以弥补请求者在其设备的 I/O 请求所等待的时间的系统定义和特定于设备的类型的值。 有关提升值，请参阅 wdm.h 中或 Ntddk.h。

更高级别的驱动程序将相同的应用*PriorityBoost*作为其各自基础设备驱动程序拨打电话时**IoCompleteRequest**。

### <a name="effect-of-calling-iocompleterequest"></a>调用 IoCompleteRequest 的效果

当驱动程序调用**IoCompleteRequest**，I/O 管理器填充数字零调用下一步的更高级别的驱动程序，如果有已设置了该驱动程序的 I/O 堆栈位置*IoCompletion*到例程针对 IRP 调用。

更高级别的驱动程序的*IoCompletion*例程可以检查仅 IRP 的 I/O 状态块以确定如何所有较低的驱动程序处理请求。

调用方**IoCompleteRequest**必须尝试访问刚完成 IRP。 这类尝试是编程错误导致系统崩溃。

 

 




