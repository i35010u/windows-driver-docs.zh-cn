---
title: 使用驱动程序创建的线程管理联锁队列
description: 使用驱动程序创建的线程管理联锁队列
ms.assetid: e2712d52-e98a-4450-b010-9278db3a7a1e
keywords:
- 互锁的 IRP 队列 WDK 内核
- 驱动程序创建的线程 WDK Irp
- 双向链接的 Irp WDK 内核
- 驱动程序专用线程 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b9f3bdcbcb9ce3964fa5df67f4661ee146a89a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386015"
---
# <a name="managing-interlocked-queues-with-a-driver-created-thread"></a>使用驱动程序创建的线程管理联锁队列





新的驱动程序应使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)framework 优先于在本部分中所述的方法。

像系统软盘控制器驱动程序的驱动程序与设备专用线程，而非[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程中，通常管理其自身中的队列的 Irp 双向链接的联锁队列。 在设备上完成工作时，驱动程序的线程从其互锁队列拉取 Irp。

一般情况下，该驱动程序必须管理与它对线程和其他驱动程序例程之间共享任何资源的线程的同步。 该驱动程序还必须具有某种方式来通知其驱动程序创建的线程 Irp 进行排队。 通常情况下，线程调度程序对象存储在设备扩展，直到驱动程序的调度例程的调度程序对象后设置为用信号通知状态将 IRP 插入到互锁队列上等待。

驱动程序的调度例程调用时，每个检查输入 IRP 的 I/O 堆栈位置中的参数和，如果有效，队列请求进行进一步处理。 对于每个 IRP 排队发送至驱动程序专用线程，调度例程应设置其线程需要处理的任何上下文 IRP 之前调用**ExInterlockedInsert*Xxx*列表**。 在每个 IRP 的驱动程序的 I/O 堆栈位置提供设备扩展的目标设备对象，其中驱动程序可以共享上下文信息与它的线程，因为线程从队列中删除每个 IRP 的驱动程序的线程访问。

队列可取消 Irp 的驱动程序必须实现[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程。 由于以异步方式取消 Irp，必须确保您的驱动程序可避免可能会导致的争用情况。 请参阅[同步 IRP 取消](synchronizing-irp-cancellation.md)有关取消 Irp 和技术，以避免其与相关联的争用条件的详细信息。

任何驱动程序创建的线程运行在 IRQL = 被动\_级别和在以前设置驱动程序调用时的基本运行时优先级[ **PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)。 线程的调用[ **ExInterlockedRemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545427)暂时引发调度到 IRQL\_IRP 正在删除从驱动程序时，当前的处理器上的级别的内部队列。 原始的 IRQL 恢复到被动\_级别从此调用返回。

**任何驱动程序线程 （或驱动程序所提供的工作线程回调） 必须仔细管理它运行于 Irql。例如，请考虑以下情况：**

-   由于系统线程通常运行在 IRQL = 被动\_级别，它是驱动程序线程等待内核定义调度程序对象设置为终止状态。

    例如，设备专用线程可能会等待其他驱动程序，以满足事件并完成一定数量的部分传输与设置的线程的 Irp [ **IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)。

-   但是，设备专用线程 IRQL 当前处理器上使之前必须提升它调用某些支持例程。

    例如，如果驱动程序使用 DMA，其设备专用的线程必须嵌套到其调用[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)并[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)调用之间[ **KeRaiseIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)并[ **KeLowerIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)因为这些例程和某些其他支持例程 DMA 操作必须在调用在 IRQL = 调度\_级别。

    请记住， [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程运行在调度\_级别，因此使用 DMA 的驱动程序无需调用**Ke*Xxx*Irql**从例程他们*StartIo*例程。

-   驱动程序创建线程可以访问可分页的内存，因为它运行在 nonarbitrary 线程上下文中 （自身） 在 IRQL = 被动\_级别，但许多其他标准驱动程序例程运行在 IRQL &gt;= 调度\_级别。 如果驱动程序创建的线程分配一个此类例程可以访问的内存，它必须从非分页缓冲池分配内存。 例如，如果设备专用线程分配驱动程序的 ISR 将更高版本访问任何缓冲区或[ *SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)， [ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)， [ *AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_list_control)， [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)， [ *DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)， [ *CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)， [ *IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)， [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)，或在更高级别的驱动程序[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，线程分配内存不能为可分页。

-   如果驱动程序保持共享的状态信息或在设备扩展中，驱动程序线程的资源 (如*StartIo*例程) 必须同步其访问物理设备和共享数据使用驱动程序的其他例程的访问相同的设备、 内存位置或资源。

    如果线程与 ISR 共享设备或状态，它必须使用[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)调用驱动程序提供[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)例程进行编程设备或访问共享的状态。 请参阅[使用临界区](using-critical-sections.md)。

    如果线程共享状态或资源与非 ISR 的例程，该驱动程序必须保护的共享的状态或使用该驱动程序为其提供存储驱动程序初始化 executive 旋转锁的资源。 有关详细信息，请参阅[旋转锁](spin-locks.md)。

使用慢速设备驱动程序线程的设计折衷方案的详细信息，请参阅[轮询设备](avoid-polling-devices.md)。 另请参阅[管理硬件优先级](managing-hardware-priorities.md)。 有关特定支持例程于 Irql 的特定信息，请参阅例程的参考页。

 

 




