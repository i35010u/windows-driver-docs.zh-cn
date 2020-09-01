---
title: 如何在 Dispatch 例程中完成 IRP
description: 如何在 Dispatch 例程中完成 IRP
ms.assetid: b29da791-e768-4f67-8e85-6cfbeca97220
keywords:
- 完成 Irp WDK 内核，调度例程
- 调度例程 WDK 内核，完成 Irp
- 状态信息 WDK Irp
- I/o 状态阻止 WDK 内核
- 状态阻止 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2090667e11aba11d206b4b863d31c3e7dafdac26
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188581"
---
# <a name="how-to-complete-an-irp-in-a-dispatch-routine"></a>如何在 Dispatch 例程中完成 IRP





如果输入 IRP 可以立即完成，则调度例程会执行以下操作：

1.  用适当的值设置 IRP 的 i/o 状态块的 **状态** 和 **信息** 成员，一般为：

    -   调度例程会将**状态**设置为 " \_ 成功" 或 "错误" (状态 \_ *XXX*) ，这可以是通过调用支持例程返回的值，也可以是较低的驱动程序对某些同步请求返回的值。

        如果较低级别的驱动程序返回状态 \_ "挂起"，则较高级别的驱动程序不应为 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，但有一种情况例外：较高级别的驱动程序可以使用事件在其 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程与其调度例程之间进行同步，在这种情况下， *IoCompletion* 例程会向事件发出信号，并返回 \_ \_ \_ 所需的状态更多处理。 调度例程等待事件，然后调用 **IoCompleteRequest** 来完成 IRP。

    -   如果满足了传输数据（如读取或写入请求）的请求，则它会将 **信息** 设置为成功传输的字节数。

    -   它将 **信息** 设置为一个值，该值根据特定的请求（对于其完成状态为 "成功" 的 irp）而变化 \_ 。

    -   它将**信息**设置为一个值，该值根据其完成时的特定请求和警告状态 XXX 而变化 \_ *XXX*。 例如，它会将 **信息** 设置为传输的字节数，作为状态 \_ 缓冲区 \_ 溢出。

    -   通常情况下，它会将**信息**设置为零，使其完成时出现错误状态 \_ *XXX*。

2.  调用 **IoCompleteRequest** ，并将 *PriorityBoost* = IO 与 IRP 一起调用， \_ 无 \_ 增量。

3.  返回 \_ 在 i/o 状态块中已设置的相应状态*XXX* 。 请注意，对 **IoCompleteRequest** 的调用会使给定的 IRP 无法由调用方访问，因此来自调度例程的返回值不能从已经完成的 irp 的 i/o 状态块设置。

**遵循以下实现准则，使用 IRP 调用 IoCompleteRequest：**

在调用 **IoCompleteRequest**之前，始终释放驱动程序) 的任何自旋锁 (。

完成 IRP 需要不确定的时间，特别是在一系列分层驱动程序中。 此外，如果较高级别的驱动程序的 *IoCompletion* 例程将 IRP 向下发送到持有自旋锁的较低驱动程序，则可能会发生死锁。

 

