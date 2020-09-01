---
title: 同步中断代码
description: 同步中断代码
ms.assetid: a24477dc-f75d-4ab6-8695-d8a85247e276
keywords:
- 硬件中断 WDK KMDF，同步
- 中断 WDK KMDF，同步
- 同步 WDK 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53687aa92d34218feac175c171518f5961172bd3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191987"
---
# <a name="synchronizing-interrupt-code"></a>同步中断代码


以下因素会使处理多处理器系统上的硬件中断的驱动程序代码复杂化：

-   设备每发生一次中断，都提供中断特定的信息，这是因为它可以在下一次中断设备时被覆盖。

-   设备在相对较高的 IRQLs 处中断，其中断服务例程 (Isr) 可以中断其他驱动程序代码的执行。

-   对于 DIRQL 中断，ISR 必须在 DIRQL 时运行，同时保留驱动程序提供的自旋锁，使 ISR 可以在保存可变信息时阻止其他中断。 DIRQL 可防止当前处理器中断，并且旋转锁定可防止其他处理器中断。

-   ISR 必须迅速运行，因为设备在 ISR 执行时无法中断。 长时间的 ISR 执行时间可能会导致系统变慢或可能导致数据丢失。

-    (DPC) 例程的 ISR 和延迟过程调用通常都必须访问 ISR 存储设备的可变数据的存储区域。 这些例程必须彼此同步，以使它们不会同时访问存储区。

由于所有这些因素，编写处理中断的驱动程序代码时，必须使用以下规则：

-   仅 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数可访问可变中断数据，如包含中断信息的设备寄存器。

    [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数应将可变数据移到驱动程序定义的中断数据缓冲区，驱动程序的[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数、 [*EvtInterruptWorkItem*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数或多个[*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数可以访问。

    如果驱动程序为其中断对象提供 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtInterruptWorkItem*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) 回调函数，则存储中断数据的最佳位置是中断对象的 [上下文空间](framework-object-context-space.md)。 中断对象的回调函数可以通过使用其接收的对象句柄来访问对象的上下文空间。

    如果驱动程序为每个[*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数提供多个[*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数，则可以在每个 DPC 对象的上下文空间中存储中断数据。

-   所有访问中断数据缓冲区的驱动程序代码都必须进行同步，以便一次只有一个例程访问数据。

    对于 DIRQL 中断对象， [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数在保存中断对象驱动程序提供的自旋锁时，以 IRQL = DIRQL 访问此数据缓冲区。 因此，访问该缓冲区的所有例程还必须在持有自旋锁时在 DIRQL 运行。  (通常，中断的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 回调函数是必须访问缓冲区的唯一其他例程。 ) 

    除 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数外，所有访问中断数据缓冲区的例程都必须执行下列操作之一：

    -   调用 [**WdfInterruptSynchronize**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize) 可计划访问中断数据缓冲区的 [*EvtInterruptSynchronize*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_synchronize) 回调函数。
    -   放置在对 [**WdfInterruptAcquireLock**](/previous-versions/ff547340(v=vs.85)) 和 [**WdfInterruptReleaseLock**](/previous-versions/ff547376(v=vs.85))的调用之间访问中断数据缓冲区的代码。

    这两种方法都允许 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EVTDPCFUNC*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 函数访问 DIRQL 的中断数据，同时保留中断的旋转锁。 DIRQL 可防止当前处理器中断，并且旋转锁定可防止其他处理器中断。

    如果你的设备支持多个中断向量或消息，并且你想要同步驱动程序对这些中断的处理，则可以为多个 DIRQL 中断对象分配一个自旋锁。 该框架确定中断集的最高 DIRQL，并且它始终获取该 DIRQL 的自旋锁，以便该集中的任何中断向量或消息不会中断同步的代码。

    对于 [被动级别中断对象](supporting-passive-level-interrupts.md)，框架在以 IRQL = 被动级别调用驱动程序的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数之前，将获取被动级别中断锁 \_ 。 因此，所有访问缓冲区的例程都必须获取中断锁或内部同步缓冲区访问。 通常，中断的 [*EvtInterruptWorkItem*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) 回调函数是访问缓冲区的唯一其他例程。 有关从 *EvtInterruptWorkItem* 回调函数获取中断锁的信息，请参阅该页的 "备注" 部分。

    还可以通过为多个被动级别中断对象分配一个等待锁，来同步驱动程序对多个中断向量的处理。

-   如果处理 DIRQL 中断的部分代码必须以 IRQL = 被动 \_ 级别运行，则 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 回调函数可以创建一个或多个 [工作项](using-framework-work-items.md) ，以便代码将作为 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数运行。

    或者，在 KMDF 版本1.11 及更高版本中，驱动程序可以通过调用 [**WdfInterruptQueueWorkItemForIsr**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)来请求中断工作项。  (回忆，驱动程序的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数可以调用 **WdfInterruptQueueWorkItemForIsr** 或 [**WdfInterruptQueueDpcForIsr**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)，但不能同时调用两者。 ) 

-   如果对驱动程序的[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)和[*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数以及与设备关联的其他回调函数进行同步时，您的驱动程序可以将该函数的**AutomaticSerialization**成员设置为 TRUE，并将其设置为**TRUE** 。 [** \_ \_ **](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config) [** \_ \_ **](/windows-hardware/drivers/ddi/wdfdpc/ns-wdfdpc-_wdf_dpc_config) 或者，驱动程序可以使用 [框架自旋锁](using-framework-locks.md#framework-spin-locks)。 将 **AutomaticSerialization** 成员设置为 **TRUE** (不会将 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数与其他回调函数同步。 如本主题前面所述，使用 [**WdfInterruptSynchronize**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize) 或 [**WdfInterruptAcquireLock**](/previous-versions/ff547340(v=vs.85)) 来同步 *EvtInterruptIsr* 回调函数。 ) 

有关同步驱动程序例程的详细信息，请参阅 [基于框架的驱动程序的同步技术](./using-automatic-synchronization.md)。

 

