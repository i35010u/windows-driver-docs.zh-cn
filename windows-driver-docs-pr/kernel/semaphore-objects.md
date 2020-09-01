---
title: 信号灯对象
description: 信号灯对象
ms.assetid: e6703c39-3b47-4d3b-86e7-bf2bf37af493
keywords:
- 内核调度程序对象 WDK，信号对象
- 调度程序对象 WDK 内核，信号对象
- 信号对象 WDK 内核
- KeInitializeSemaphore
- 等待信号对象
- KeReleaseSemaphore
- 统计信号量 WDK 内核
- 二进制信号量 WDK 内核
- 等待状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99318cdf70a2808836be513af6e72d1758744ad2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191924"
---
# <a name="semaphore-objects"></a>信号灯对象





任何驱动程序都可以使用信号灯对象在其驱动程序创建的线程与其他驱动程序例程之间同步操作。 例如，如果驱动程序没有未完成的 i/o 请求，驱动程序专用线程可能会将其自身置于等待状态，并且在队列 IRP 之后，驱动程序的调度例程可能将信号量设置为终止状态。

在请求 i/o 操作的线程的上下文中运行的最高级别的驱动程序的调度例程可能使用信号量来保护在调度例程间共享的资源。 用于同步 i/o 操作的较低级别的驱动程序调度例程还可能使用信号量来保护在调度例程子集或使用驱动程序创建的线程之间共享的资源。

使用信号灯对象的任何驱动程序都必须在等待或释放信号量之前调用 [**KeInitializeSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializesemaphore) 。 下图说明了具有线程的驱动程序如何使用信号量对象。

![说明等待信号灯对象的关系图](images/3semobj.png)

如上图所示，此类驱动程序必须为应驻留的信号灯对象提供存储。 驱动程序可以使用驱动程序创建的设备对象的 [设备扩展](device-extensions.md) ，如果控制器扩展使用 [控制器对象](./introduction-to-controller-objects.md)或由驱动程序分配的非分页池，则可以使用控制器扩展。

当驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程调用 **KeInitializeSemaphore**时，它必须为信号灯对象传递指向驱动程序的驻留存储的指针。 此外，调用方必须指定信号量对象的 *计数* （如上图所示），以确定) 的初始状态 (非零值。

调用方还必须指定信号量的限制，可以为以下 *值* 之一：

-   **限制 = 1**

    如果此信号灯设置为 "已终止" 状态，则等待信号量设置为 "已终止" 状态的单个线程将变为符合执行的条件，并可访问受信号量保护的任何资源。

    这种类型的信号量也称为 *二进制信号量* ，因为线程具有或没有对受信号保护资源的独占访问权限。

-   **限制 &gt; 1**

    如果此信号灯设置为 "已终止" 状态，则一些等待信号灯对象设置为 "已终止" 状态的线程将变为符合执行的条件，并可访问受信号量保护的任何资源。

    这种类型的信号量称为 *计数信号量* ，因为将信号量设置为 "已终止" 状态的例程还指定了多少个等待线程可以将其状态从 "等待" 状态更改为 "就绪"。 此类等待线程的数量可能是初始化信号量时设置的 *限制* ，或者是小于此预设 *限制*的某个数字。

很少有设备或中间驱动程序具有单个驱动程序创建的线程;甚至更少的一组线程可能会等待获取或释放信号量。 系统提供的几个驱动程序使用信号量对象，而此类对象只使用二进制信号量。 尽管二进制信号量在功能上可能与 [互斥体对象](mutex-objects.md)相似，但二进制信号量不提供对在 SMP 计算机中运行的系统线程的死锁的内置保护。

在加载了具有初始化信号量的驱动程序后，它可以在保护共享资源的信号量上同步操作。 例如，具有设备专用线程的驱动程序（如系统软盘控制器驱动程序）可在信号量上同步 IRP 队列，如前图所示：

1.  线程调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) ，该指针指向已初始化的信号灯对象的驱动程序提供的存储，以将其本身置于等待状态。

2.  Irp 开始需要设备 i/o 操作。 驱动程序的调度例程将每个此类 IRP 插入到 "旋转锁定" 控件下的互锁队列，并使用指向信号量对象的指针调用 [**KeReleaseSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore) ，由驱动程序为线程确定的优先级提升 (*增量*，如前面的图) 所示，将在每个 IRP 排队时添加到信号量的计数的 *调整* ，并将布尔 *等待* 设置为 **FALSE**。 非零信号量计数将信号灯对象设置为终止状态，从而将等待线程的状态更改为 "就绪"。

3.  处理器可用时，内核会立即调度线程以执行：也就是说，具有较高优先级的其他线程目前处于 "就绪" 状态，并且没有要在更高的 IRQL 上运行的内核模式例程。

    该线程从 "旋转锁定控制" 下的 "互锁" 队列中删除 IRP，将其传递给其他驱动程序例程进行进一步处理，并再次调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 。 如果信号量仍设置为 "已终止" 状态 (即，其计数保持非零值，表示驱动程序的互锁队列) 中有更多的 Irp，则内核将再次更改线程的状态 "等待就绪"。

    通过以这种方式使用计数信号量，此类驱动程序线程 "知道" 只要运行该线程，就会从联锁队列中删除 IRP。

如果调用 [**KeReleaseSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore) 并将 *Wait* 参数设置为 **TRUE** ，则表示调用方应立即调用 **KeWait*Xxx*对象** () 支持从 **KeReleaseSemaphore**返回的例程。

请考虑以下将 *Wait* 参数设置为 KeReleaseSemaphore 的准则：

以 IRQL 被动级别运行的可分页线程或可分页驱动程序例程 \_ 不应调用 **KeReleaseSemaphore** ，并将 *Wait* 参数设置为 **TRUE**。 如果调用方在对 **KeReleaseSemaphore** 和 **KeWait*Xxx*对象** 的调用之间分页 () ，则这种调用将导致严重的页错误。

以 IRQL 大于被动级别运行的任何标准驱动程序例程都 \_ 不会在不关闭系统的情况下等待任何调度程序对象上的非零间隔; 有关详细信息，请参阅 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md) 。 但是，在小于或等于调度级别的 IRQL 下运行时，此类例程可以调用 **KeReleaseSemaphore** \_ 。

有关标准驱动程序例程运行的 IRQLs 的摘要，请参阅 [管理硬件优先级](managing-hardware-priorities.md)。 有关特定支持例程的 IRQL 要求，请参阅例程的参考页。

 

