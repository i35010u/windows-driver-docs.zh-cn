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
ms.openlocfilehash: fdd29ab44470cd5db824bdf193ac6d6dabb00962
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192472"
---
# <a name="implementing-an-iocompletion-routine"></a>实现 IoCompletion 例程





进入时， [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程接收 *上下文* 指针。 当调度例程调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)时，它可以提供 *上下文* 指针。 此指针可以引用 *IoCompletion* 例程处理 IRP 所需的任何驱动程序确定的上下文信息。 请注意，上下文区域无法进行分页，因为在 IRQL = 调度级别可以调用 *IoCompletion* 例程 \_ 。

**请考虑以下 IoCompletion 例程实现准则：**

-   *IoCompletion*例程可以检查 IRP 的[i/o 状态块](i-o-status-blocks.md)，以确定 i/o 操作的结果。

-   如果使用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 或 [**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)的调度例程分配了输入 IRP，则 *IoCompletion* 例程必须调用 [**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp) ，以释放该 irp，这在完成原始 irp 之前最好。

    -   在释放相应的 IRP 之前， *IoCompletion* 例程必须释放分配给驱动程序分配的 irp 的调度例程。

        例如，如果调度例程分配了 [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl) 的 MDL，并为它分配的部分传输 IRP 调用 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) ，则 *IoCompletion* 例程必须使用 [**IoFreeMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl)释放 mdl。 如果它分配资源来维护有关原始 IRP 的状态，则它必须释放这些资源，最好是在通过原始 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 之前，并在它返回控制权之前肯定的。

        通常，在释放或完成 IRP 之前， *IoCompletion* 例程应释放调度例程分配的每个 IRP 资源。 否则，驱动程序必须保持对要释放的 *资源的状态* ，然后才能通过完成原始请求来返回控件。

    -   如果 *IoCompletion* 例程无法完成状态为 "成功" 的原始 irp \_ ，则必须将原始 irp 中的 i/o 状态块设置为驱动程序分配的 irp 中返回的值，导致 *IoCompletion* 例程对原始请求失败。

    -   如果*IoCompletion*例程将完成状态为 "挂起" 的原始请求 \_ ，则在调用**IoCompleteRequest**之前，它必须与原始 IRP 一起调用[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)。

    -   如果*IoCompletion*例程必须使原始 IRP 失败，并出现错误状态 \_ *XXX*，则它可能会[记录一个错误](logging-errors.md)。 但是，基础设备驱动程序负责记录发生的任何设备 i/o 错误，因此， *IoCompletion* 例程通常不会记录错误。

    -   *IoCompletion*例程处理并释放了驱动程序分配的 IRP 后，例程必须返回状态为 " \_ 需要更多处理" 的控制 \_ \_ 。

        返回状态 \_ \_ \_ *IoCompletion* 例程所需的更多处理，forestalls 为驱动程序分配和释放 IRP 的 i/o 管理器完成处理。 对 **IoCompleteRequest** 的第二次调用会导致 i/o 管理器恢复调用 IRP 的完成例程，从立即返回状态 \_ 更多需要处理的例程开始，开始 \_ \_ 。

-   如果 *IoCompletion* 例程重复使用传入的 IRP 将一个或多个请求发送到较低的驱动程序，或者如果例程重试失败的操作，则它应更新 *IoCompletion* 例程针对每次重新使用或重试 IRP 而维护的所有上下文。 然后，它可以再次设置下一个较低的驱动程序的 i/o 堆栈位置，并调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 的入口点，并为 IRP 调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。

    -   *IoCompletion*例程不应在每次重新使用或重试 IRP 时调用[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)。

        调度例程已将原始 IRP 标记为挂起。 直到链中的所有驱动程序都完成具有 **IoCompleteRequest**的原始 IRP 后，它仍处于挂起状态。

    -   在重试请求之前， *IoCompletion*例程应重置状态为 "成功" 的 i/o 状态块， \_ 并在保存返回的**Status**错误信息后重置为零。 **Information**

        对于每次重试， *IoCompletion* 例程通常会减少调度例程设置的重试计数。 通常，如果重试次数有限， *IoCompletion* 例程必须调用 **IOCOMPLETEREQUEST** 以使 IRP 失败。

    -   *IoCompletion*例程在使用重新使用 \_ \_ \_ 或重试的 IRP 调用[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)和[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)后，必须返回状态更多所需的处理。

        返回状态 \_ \_ \_ *IoCompletion* 例程所需的更多处理，forestalls i/o 管理器重新使用或重试 IRP 的完成处理。

    -   如果 *IoCompletion* 例程无法完成状态为 "成功" 的原始 IRP \_ ，则它必须保留由较低版本的驱动程序返回的 i/o 状态块，以便重用或重试操作导致 *IoCompletion* 例程失败 IRP。

    -   如果*IoCompletion*例程将完成状态为 "挂起" 的原始请求 \_ ，则在调用**IoCompleteRequest**之前，它必须与原始 IRP 一起调用**也**。
    -   如果*IoCompletion*例程必须使原始 IRP 失败，并出现错误状态 \_ *XXX*，则它可能会[记录一个错误](logging-errors.md)。 但是，基础设备驱动程序负责记录发生的任何设备 i/o 错误，因此， *IoCompletion* 例程通常不会记录错误。

-   如果任何驱动程序在 IRP 中设置*IoCompletion*例程，然后将 irp 向下传递到较低的驱动程序，则应在*IoCompletion*例程中检查**irp- &gt; PendingReturned**标志。 如果设置了标志， *IoCompletion* 例程必须通过 IRP 调用 **也** 。 但请注意，通过 IRP 并等待事件等待的驱动程序不应将 IRP 标记为 "挂起"。 相反，它的 *IoCompletion* 例程应向事件发出信号，并使状态返回 \_ 更多 \_ \_ 所需的处理。

-   *IoCompletion*例程必须释放调度例程分配用于处理原始 irp 的任何资源，最好是在*IoCompletion*例程调用**IoCompleteRequest**和原始 irp 之前，并在*IoCompletion*例程从完成原始 irp 之前返回控制之前。

如果任何更高级别的驱动程序在原始 IRP 中设置了其*IoCompletion*例程，则在调用所有较低级别驱动程序的*IoCompletion*例程之前，不会调用该驱动程序的*IoCompletion*例程。

### <a name="supplying-a-priority-boost-in-calls-to-iocompleterequest"></a>在对 IoCompleteRequest 的调用中提供优先级提升

如果最低级别的设备驱动程序可以在其调度例程中完成 IRP，则它会调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ， *PriorityBoost* 的 IO \_ 无 \_ 增量。 不需要运行时优先级增加，因为驱动程序可以假定原始请求方不会等待其 i/o 操作完成。

否则，最低级别的驱动程序会提供系统定义的特定于设备类型的值，以弥补请求者在其设备 i/o 请求上等待的时间。 有关提升值，请参阅 Wdm 或 Ntddk。

更高级别的驱动程序在调用**IoCompleteRequest**时，应用与其各自的基础设备驱动程序相同的*PriorityBoost* 。

### <a name="effect-of-calling-iocompleterequest"></a>调用 IoCompleteRequest 的效果

当驱动程序调用 **IoCompleteRequest**时，i/o 管理器将使用零填充该驱动程序的 i/o 堆栈位置，然后再调用下一个较高级别的驱动程序（如果有），该驱动程序已设置为 IRP 调用 *IoCompletion* 例程。

较高级别的驱动程序的 *IoCompletion* 例程只能检查 IRP 的 i/o 状态块，以确定所有较低版本的驱动程序如何处理该请求。

**IoCompleteRequest**的调用方不能尝试访问刚完成的 IRP。 此类尝试是导致系统崩溃的编程错误。

 

