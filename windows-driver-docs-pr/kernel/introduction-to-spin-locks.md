---
title: 自旋锁简介
description: 自旋锁简介
keywords:
- KSPIN_LOCK
- executive 旋转锁定 WDK 内核
- 中断自旋锁定 WDK 内核
- 排队自旋锁 WDK 内核
- 旋转锁定 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a90c668cfb34319155d44e6b4555cc8d1a981a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838881"
---
# <a name="introduction-to-spin-locks"></a>自旋锁简介





自旋锁是内核定义的内核模式同步机制，作为不透明类型导出： KSPIN \_ LOCK。 自旋锁可用于保护共享数据或资源，使其能够以并发方式同时在 SMP 计算机上并发执行和以 IRQL &gt; = 调度 \_ 级别执行。

许多组件使用自旋锁（包括驱动程序）。 任何类型的驱动程序都可以使用一个或多个 *执行自旋锁*。 例如，大多数文件系统在文件系统驱动程序的 (FSD 的) 设备扩展中使用联锁工作队列来存储由文件系统的工作线程回调例程和 FSD 处理的 Irp。 联锁工作队列受 executive 旋转锁保护，该锁可解决 FSD 中尝试将 Irp 插入队列的争用，以及同时尝试删除 Irp 的所有线程。 作为另一个示例，系统软盘控制器驱动程序使用两个执行自旋锁。 一个 executive 旋转锁可保护与此驱动程序的设备专用线程共享的联锁工作队列;另一种方法是保护由三个驱动程序例程共享的计时器对象。

适用于 Microsoft Windows XP 和更高版本 Windows 的驱动程序可以使用 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 和 [**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 获取并释放作为 *排队旋转锁* 的旋转锁。 对于多处理器计算机上的高争用锁，排队自旋锁比普通旋转锁提供更好的性能。 有关详细信息，请参阅 [排队自旋锁](queued-spin-locks.md)。 适用于 Windows 2000 的驱动程序可以使用 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 和 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 获取并释放旋转锁定作为普通旋转锁。

为了同步访问简单的数据结构，驱动程序可以使用任何 **ExInterlocked * Xxx*** 例程来确保对数据结构的原子访问。 使用这些例程的驱动程序无需显式获取或释放旋转锁。

具有 ISR 的每个驱动程序都使用 *中断自旋锁* 来保护其 ISR 与其 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程之间共享的任何数据或硬件，这些例程通常从其 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 和 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程调用。 中断自旋锁与驱动程序调用 [**IoConnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)时创建的中断对象集相关联，如注册 ISR 中所述。

**请按照以下准则来使用驱动程序中的自旋锁：**

-   提供由旋转锁保护的任何数据或资源的存储，并为常驻系统中的相应自旋锁 (非分页池，如 [虚拟内存空间和物理内存](overview-of-windows-memory-space.md) 图) 所示。 驱动程序必须为其使用的任何执行自旋锁提供存储空间。 但是，设备驱动程序无需为中断旋转锁定提供存储，除非它具有 multivector ISR 或具有多个 ISR，如注册 ISR 中所述。

-   调用 [**KeInitializeSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock) ，初始化驱动程序为其提供存储的每个自旋锁，然后使用它来同步访问它所保护的共享数据或资源。

-   调用每个支持例程，该例程在适当的 IRQL 处使用自旋锁，一般为：对于 &lt; executive 旋转锁，为调度级别，对于 \_ &lt; 与驱动程序中断对象关联的中断自旋锁，则为 DIRQL。

-   在持有自旋锁的情况下，尽可能快地执行例程来执行。 任何例程都不应将旋转锁定保留超过25微秒。

-   在持有自旋锁的情况下，切勿实现执行以下任一操作的例程：

    -   导致硬件异常或引发软件异常。

    -   尝试访问可分页内存。

    -   发出一个递归调用，该调用会导致死锁，或导致保持旋转锁的时间超过25微秒。

    -   如果执行此操作可能会导致死锁，则尝试获取另一个自旋锁。

    -   调用与上述任何规则冲突的外部例程。

 

