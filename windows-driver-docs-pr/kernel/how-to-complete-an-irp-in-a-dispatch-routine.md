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
ms.openlocfilehash: 1176863800cb93ab75e1634d2052fb6ca46cd592
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838644"
---
# <a name="how-to-complete-an-irp-in-a-dispatch-routine"></a>如何在 Dispatch 例程中完成 IRP





如果输入 IRP 可以立即完成，则调度例程会执行以下操作：

1.  用适当的值设置 IRP 的 i/o 状态块的**状态**和**信息**成员，一般为：

    -   调度例程将**状态**设置为 "成功"\_"状态" 设置为 "成功" 或相应的 "错误" （"状态\_*XXX*"），这可能是通过调用支持例程返回的值或较低的驱动程序对某些同步请求返回的值。

        如果较低级别的驱动程序返回状态\_"挂起"，则较高级别的驱动程序不应为 IRP 调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，但有一种例外情况：较高级别的驱动程序可以使用事件在其[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程和其调度例程，在这种情况下， *IoCompletion*例程向事件发出信号，并返回状态\_\_需要更多的\_处理。 调度例程等待事件，然后调用**IoCompleteRequest**来完成 IRP。

    -   如果满足了传输数据（如读取或写入请求）的请求，则它会将**信息**设置为成功传输的字节数。

    -   它将**信息**设置为一个值，该值因特定请求而异，而该 irp 完成时状态\_成功。

    -   它将**信息**设置为一个值，该值根据其完成的特定请求的特定请求而变化，并且警告状态\_*XXX*。 例如，它会将**信息**设置为传输的字节数，作为状态\_缓冲区\_溢出。

    -   通常情况下，它会将**信息**设置为零，以使其完成并且错误状态\_*XXX*。

2.  通过 IRP 和*PriorityBoost* = IO 调用**IOCOMPLETEREQUEST** ，\_没有\_递增。

3.  返回在 i/o 状态块中已设置的相应状态\_*XXX* 。 请注意，对**IoCompleteRequest**的调用会使给定的 IRP 无法由调用方访问，因此来自调度例程的返回值不能从已经完成的 irp 的 i/o 状态块设置。

**遵循以下实现准则，使用 IRP 调用 IoCompleteRequest：**

在调用**IoCompleteRequest**之前，始终释放驱动程序所持有的任何自旋锁。

完成 IRP 需要不确定的时间，特别是在一系列分层驱动程序中。 此外，如果较高级别的驱动程序的*IoCompletion*例程将 IRP 向下发送到持有自旋锁的较低驱动程序，则可能会发生死锁。

 

 




