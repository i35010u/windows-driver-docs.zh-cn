---
title: 取消 IRP 时要考虑的要点
description: 取消 IRP 时要考虑的要点
ms.assetid: 16a47033-7147-43a2-a9f8-a215f7e90ff1
keywords:
- 正在取消 Irp，准则
- 取消例程准则
- 可取消 Irp WDK 内核
- 当前状态 WDK Irp
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 61a78aae240bd690a6507e3a3ad9ec555d99f2f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369222"
---
# <a name="points-to-consider-when-canceling-irps"></a>取消 IRP 时要考虑的要点





本部分讨论了用于实现指导原则*取消*例程和处理可取消 Irp。 有关处理可取消 Irp 的详细信息，请参阅[流的队列的控制取消安全 IRP](https://go.microsoft.com/fwlink/p/?linkid=57844)。

### <a name="general-guidelines-for-all-cancel-routines"></a>所有取消例程的通用指南

I/O 管理器保存调用驱动程序的任何时间取消自旋锁*取消*例程。 因此，每个*取消*例程必须：

-   调用[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550)返回控件之前。

-   不调用[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)除非它调用**IoReleaseCancelSpinLock**第一个。

-   相互调用**IoReleaseCancelSpinLock**它对每次调用**IoAcquireCancelSpinLock**。

每次*取消*例程调用**IoReleaseCancelSpinLock**，它必须将传递到最新的调用返回的 IRQL **IoAcquireCancelSpinLock**。 发布 I/O 管理器获取的自旋锁时 (并保持时*取消*例程调用)，则*取消*例程必须传递**Irp-&gt;CancelIrql**.

驱动程序不能调用外部例程 (如**IoCompleteRequest**) 同时保留旋转锁，因为可能会导致死锁。

### <a href="" id="using-the-queue-defined-by-the-i-o-manager-"></a>使用 I/O 管理器定义的队列

除非驱动程序管理其自身内部队列的 Irp，其*取消*例程称为传入 IRP，可能是以下之一：

-   **CurrentIrp**中输入的目标设备对象

-   目标设备对象与关联的设备队列中的条目

除非驱动程序管理其自身内部队列的 Irp，其*取消*例程应调用[ **KeRemoveEntryDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553163) IRP 来测试是否为中的条目中的输入目标设备对象与关联的设备队列。 驱动程序的*取消*例程*不能*调用**KeRemoveDeviceQueue**或者**KeRemoveByKeyDeviceQueue**因为它不能假定给定的 IRP 是设备队列中的任何特定位置。

### <a name="current-state-of-the-input-irp"></a>输入 IRP 的当前状态

如果*取消*调用例程与 IRP 为其驱动程序已启动 I/O 处理，但请求将很快完成，*取消*例程应释放系统取消自旋锁和返回控件。

如果输入 IRP 的当前状态处于挂起状态，*取消*例程必须执行以下操作：

1.  设置状态与输入的 IRP I/O 状态块\_取消**状态**对于该值为零**信息**。

2.  释放任何数值调节钮锁，它持有，包括系统取消自旋锁。

3.  调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与给定 IRP。

### <a name="holding-irps-in-a-cancelable-state"></a>持有 Irp 处于可取消状态

必须调用处于可取消状态持有 IRP 的任何驱动程序例程[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) ，必须调用[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)到设置其入口点*取消*例程中。 只有这样可以该驱动程序例程调用其他支持例程如**IoStartPacket**， **IoAllocateController**，或**ExInterlockedInsert...列表**例程。

随后处理可取消 Irp 的任何驱动程序例程必须检查是否 IRP 已经开始来满足请求的操作之前已取消。 必须调用该例程**IoSetCancelRoutine**重置为其入口点*取消*到日常**NULL** IRP 中。 该例程仅然后可以开始处理输入 IRP 其 I/O。

可能需要重置的入口点例程*取消*例程中如果它，也通过 Irp 进行进一步处理 IRP 由其他驱动程序例程和这些 Irp 可能保存在可取消状态。

可取消状态中保存 IRP 任何更高级别的驱动程序必须重置其*取消*入口点**NULL**它将传递到下一步低驱动程序和 IRP 之前**IoCallDriver**.

### <a name="canceling-an-irp"></a>正在取消 IRP

任何更高级别的驱动程序可以调用[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338) IRP 分配并传递上以进行进一步处理较低级别的驱动程序的使用。 但是，此类驱动程序不能假定给定的 IRP 将完成，状态\_低级驱动程序被取消。

### <a name="synchronization"></a>同步

驱动程序可以 （或必须具体取决于它的设计） 维护其设备的扩展名来跟踪 Irp 的可取消状态中的其他状态信息。 如果此状态由驱动程序例程在 IRQL 运行共享&lt;= 调度\_级别，应使用驱动程序分配并初始化旋转锁保护的共享的数据。

该驱动程序应管理其收购和版本的系统仔细取消自旋锁和自旋锁。 它应为可能的最短时间间隔保存系统取消自旋锁。 在访问前可取消 IRP，这样的驱动程序应始终检查返回值[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)以确定是否*取消*例程已运行 （或即将运行）;如果因此，它应让*取消*例程完成 IRP。

如果设备驱动程序维护有关与其 ISR 共享的各种驱动程序例程的可取消 Irp 的状态信息，这些其他例程必须与 ISR 同步对共享状态的访问 仅驱动程序提供*SynchCritSection*例程可以访问的多处理器安全的方式与 ISR 共享状态信息。

有关详细信息，请参阅[同步技术](synchronization-techniques.md)。

 

 




