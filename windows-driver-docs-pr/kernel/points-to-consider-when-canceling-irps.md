---
title: 取消 IRP 时要考虑的要点
description: 取消 IRP 时要考虑的要点
ms.assetid: 16a47033-7147-43a2-a9f8-a215f7e90ff1
keywords:
- 取消 Irp，指导原则
- 取消例程，指导原则
- 可取消的 Irp WDK 内核
- 当前状态 WDK Irp
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 204fede34d4eee53b48e570630e45659a6dcca00
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827668"
---
# <a name="points-to-consider-when-canceling-irps"></a>取消 IRP 时要考虑的要点





本部分介绍了实现取消例程并处理可*取消*的 irp 的准则。 有关处理可取消的 Irp 的详细信息，请参阅[取消安全 Irp 队列的控制流](https://go.microsoft.com/fwlink/p/?linkid=57844)。

### <a name="general-guidelines-for-all-cancel-routines"></a>所有取消例程的一般准则

当 i/o 管理器调用驱动程序的*取消*例程时，它会保留 "取消" 自旋锁。 因此，每个*取消*例程必须：

-   在返回 control 之前调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 。

-   除非首先调用**IoReleaseCancelSpinLock** ，否则不会调用[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) 。

-   对**IoReleaseCancelSpinLock**发出的每个调用进行对**IoAcquireCancelSpinLock**的反向调用。

当*Cancel*例程每次调用**IoReleaseCancelSpinLock**时，都必须将最新调用返回的 IRQL 传递到**IoAcquireCancelSpinLock**。 当释放由 i/o 管理器获取的自旋锁（并在调用*取消*例程时保持）时，*取消*例程必须通过**Irp&gt;irp->cancelirql**。

当持有自旋锁时，驱动程序不能在例程（如**IoCompleteRequest**）的外部调用，因为可能会导致死锁。

### <a href="" id="using-the-queue-defined-by-the-i-o-manager-"></a>使用由 i/o 管理器定义的队列

除非驱动程序管理自己的 Irp 的内部队列，否则会使用传入的 IRP 调用其*取消*例程，此操作可能是以下两种情况之一：

-   输入目标设备对象中的**CurrentIrp**

-   设备队列中与目标设备对象相关联的条目

除非驱动程序管理自己的 Irp 的内部队列，否则，它的*Cancel*例程应使用输入 IRP 调用[**KeRemoveEntryDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue) ，以测试它是否是与目标设备对象相关联的设备队列中的条目。 驱动程序的*Cancel*例程*无法*调用**KeRemoveDeviceQueue**或**KeRemoveByKeyDeviceQueue** ，因为它无法假定给定的 IRP 在设备队列中的任何特定位置。

### <a name="current-state-of-the-input-irp"></a>输入 IRP 的当前状态

如果调用使用 IRP （驱动程序已经开始处理 i/o）的*取消*例程，并且该请求即将完成，则*取消*例程应释放系统取消旋转锁定并返回控制权。

如果输入 IRP 的当前状态为 "挂起"，则 "*取消*" 例程必须执行以下操作：

1.  设置输入 IRP 的 i/o 状态块，**状态为\_已取消，状态** **为零。**

2.  释放它所持有的所有旋转锁，包括系统取消旋转锁。

3.  调用具有给定 IRP 的[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

### <a name="holding-irps-in-a-cancelable-state"></a>将 Irp 置于可取消状态

保存 IRP 处于可取消状态的任何驱动程序例程都必须调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，并且必须调用[**IOSETCANCELROUTINE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)来为 IRP 中的*Cancel*例程设置其入口点。 只有这样，该驱动程序例程才能调用其他支持例程，如**IoStartPacket**、 **IoAllocateController**或**ExInterlockedInsert。列出**例程。

以后处理可取消的 Irp 的任何驱动程序例程必须检查 IRP 是否已被取消，然后才能开始操作来满足请求。 例程必须调用**IoSetCancelRoutine** ，以便将*取消*例程的入口点重置为 IRP 中的**NULL** 。 只有这样，例程才能开始对输入 IRP 进行 i/o 处理。

如果某个例程还需要为 IRP 中的 "*取消*" 例程重置入口点，则它也可能会传递 irp 以供其他驱动程序例程进一步处理，并且这些 irp 可能会处于可取消状态。

在将 IRP 传递到下一个带**IoCallDriver**的驱动程序之前，任何以可取消状态保存 irp 的高级驱动程序都必须将其*取消*入口点重置为**NULL** 。

### <a name="canceling-an-irp"></a>取消 IRP

任何较高级别的驱动程序都可以使用已分配和传递的 IRP 来调用[**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp) ，以供较低级别的驱动程序进一步处理。 但是，此类驱动程序无法假定给定的 IRP 将以较低的驱动程序取消\_状态。

### <a name="synchronization"></a>同步

驱动程序可以（或必须根据其设计）在其设备扩展中维护附加状态信息，以跟踪 Irp 的可取消状态。 如果此状态由运行的驱动程序例程共享 &lt;= 调度\_级别，则应该使用驱动程序分配的和初始化的自旋锁保护共享数据。

驱动程序应仔细管理其对系统取消旋转锁定及其自身旋转锁定的购买和版本。 它应将系统取消自旋锁的时间间隔尽可能短。 在访问可取消的 IRP 之前，此类驱动程序应始终检查[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)的返回值，以确定*取消*例程是否已在运行（或即将运行）;如果是这样，则应让*取消*例程完成 IRP。

如果设备驱动程序维护有关各种驱动程序例程与其 ISR 共享的可取消 Irp 的状态信息，则这些其他例程必须使用 ISR 同步对共享状态的访问。 只有驱动程序提供的*SynchCritSection*例程才能访问以多处理器安全方式与 ISR 共享的状态信息。

有关详细信息，请参阅[同步技术](synchronization-techniques.md)。

 

 




