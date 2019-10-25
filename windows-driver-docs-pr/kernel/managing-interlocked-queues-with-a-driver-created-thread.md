---
title: 使用驱动程序创建的线程管理联锁队列
description: 使用驱动程序创建的线程管理联锁队列
ms.assetid: e2712d52-e98a-4450-b010-9278db3a7a1e
keywords:
- 联锁 IRP 将 WDK 内核排队
- 驱动程序创建的线程 WDK Irp
- 双重链接的 Irp WDK 内核
- 驱动程序专用线程 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6741447d1b52b83b6267d580064c89d3cd61921c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838548"
---
# <a name="managing-interlocked-queues-with-a-driver-created-thread"></a>使用驱动程序创建的线程管理联锁队列





新驱动程序应按照本部分中所述的方法优先使用 "[取消安全 IRP 队列](cancel-safe-irp-queues.md)框架"。

与系统软盘控制器驱动程序一样，驱动程序具有设备专用线程，而不是[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，通常在双向链接的联锁队列中管理自己的 irp 队列。 当设备上有工作要完成时，驱动程序的线程会从其联锁队列中提取 Irp。

通常，驱动程序必须管理与其线程的同步，使其能够与线程和其他驱动程序例程之间共享的任何资源进行同步。 驱动程序还必须有一种方法来通知其由驱动程序创建的线程，使 Irp 排队。 通常情况下，线程会等待存储在设备扩展中的调度程序对象，直到驱动程序的调度例程在将 IRP 插入到联锁队列后，将发送器对象设置为终止状态。

如果调用了驱动程序的调度例程，则每个例程都会检查输入 IRP 的 i/o 堆栈位置中的参数，如果这些参数有效，将对请求排队以进行进一步处理。 对于排队到驱动程序专用线程的每个 IRP，调度例程应设置其线程在调用**ExInterlockedInsert*Xxx*列表**之前需要处理该 irp 的任何上下文。 驱动程序的每个 IRP 中的驱动程序 i/o 堆栈位置使驱动程序的线程可以访问目标设备对象的设备扩展，其中，驱动程序可以与线程共享上下文信息，因为该线程从队列中删除每个 IRP。

排队可取消的 Irp 的驱动程序必须实现[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。 由于 Irp 是异步取消的，因此您必须确保您的驱动程序可避免出现可能产生的争用情况。 有关与取消 Irp 关联的争用条件的详细信息，请参阅[同步 IRP 取消](synchronizing-irp-cancellation.md)。

任何驱动程序创建的线程都以 IRQL = 被动\_级别运行，并在以前在驱动程序调用[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)时设置的基本运行时优先级运行。 在从驱动程序的内部队列中删除 IRP 时，该线程对[**ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)的调用将暂时引发 IRQL 以调度当前处理器上的\_级别。 从此调用返回时，原始 IRQL 会恢复到被动\_级别。

**任何驱动程序线程（或驱动程序提供的工作线程回调）都必须仔细管理其运行所在的 IRQLs。例如，请考虑以下事项：**

-   由于系统线程通常以 IRQL = 被动\_级别运行，因此驱动程序线程可能会等待将内核定义的调度程序对象设置为终止状态。

    例如，设备专用线程可能会等待其他驱动程序满足某个事件，并完成线程使用[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)设置的部分部分传输 irp。

-   但是，这种专用于设备的线程在调用某些支持例程之前必须在当前处理器上引发 IRQL。

    例如，如果驱动程序使用 DMA，则其专用于设备的线程必须在对[**KeRaiseIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)和[**KeLowerIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)的调用之间嵌套其对[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)和[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)的调用，因为这些例程和其他例程DMA 操作的支持例程必须以 IRQL = 调度\_级别进行调用。

    请记住， [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程在调度\_级别运行，因此使用 DMA 的驱动程序无需从其*StartIo*例程调用**Ke*Xxx*Irql**例程。

-   驱动程序创建的线程可以访问可分页内存，因为它以 IRQL = 被动\_级别在 nonarbitrary 线程上下文中运行，但许多其他标准驱动程序例程以 IRQL &gt;= 调度\_级别运行。 如果驱动程序创建的线程分配可以通过此类例程访问的内存，则它必须从非分页池分配内存。 例如，如果设备专用线程分配了驱动程序的 ISR 或[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)、 [*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)、 [*AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)、 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)[*以后将访问的任何缓冲区，CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)、 [*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)、 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)，或在较高级别的驱动程序[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中，无法对线程分配的内存进行分页。

-   如果驱动程序在设备扩展中维护共享状态信息或资源，则驱动程序线程（如*StartIo*例程）必须将其对物理设备的访问权限与访问同一设备的驱动程序的其他例程同步到共享数据、内存位置或资源。

    如果该线程与 ISR 共享设备或状态，则必须使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用驱动程序提供的[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程来对设备进行编程或访问共享状态。 请参阅[使用关键部分](using-critical-sections.md)。

    如果该线程与 ISR 以外的其他例程共享状态或资源，则驱动程序必须使用驱动程序为其提供存储的驱动程序初始化的执行自旋锁来保护共享状态。 有关详细信息，请参阅[自旋锁](spin-locks.md)。

有关对慢速设备使用驱动程序线程的设计折衷的详细信息，请参阅对[设备进行轮询](avoid-polling-devices.md)。 另请参阅[管理硬件优先级](managing-hardware-priorities.md)。 有关特定支持例程的 IRQLs 的特定信息，请参阅例程的参考页。

 

 




