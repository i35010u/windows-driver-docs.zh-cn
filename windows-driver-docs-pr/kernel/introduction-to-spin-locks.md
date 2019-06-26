---
title: 自旋锁简介
description: 自旋锁简介
ms.assetid: a37c0db4-ff9c-4958-a9f4-62b671458d03
keywords:
- KSPIN_LOCK
- executive 自旋锁 WDK 内核
- 中断自旋锁 WDK 内核
- 排队自旋锁 WDK 内核
- 数值调节钮锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: aed4e95e22e9105fe01b303f649e03fe3e9cca95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369912"
---
# <a name="introduction-to-spin-locks"></a>自旋锁简介





自旋锁是内核定义，仅限内核模式同步机制，导出为不透明类型：KSPIN\_锁。 旋转锁可用于防止同时访问共享的数据或资源的并发和 IRQL 在可以执行的例程&gt;= 调度\_级别 SMP 计算机中。

许多组件使用数值调节钮锁，其中包括驱动程序。 任何类型的驱动程序可能会使用一个或多个*executive 自旋锁*。 例如，大多数文件系统中使用互锁的工作队列中的文件系统驱动程序的 (FSD) 设备扩展存储的文件系统的工作线程回调例程和 FSD 处理 Irp。 互锁的工作队列受保护的 executive 自旋锁，解析尝试将 Irp 插入到队列和任何线程同时尝试删除 Irp FSD 间的争用。 另举一例，系统软盘控制器驱动程序使用两个 executive 自旋锁。 个 executive 自旋锁来保护与此驱动程序的设备专用线程，则共享互锁的工作队列其他保护共享的三个驱动程序例程的计时器对象。

Microsoft Windows XP 和更高版本的 Windows 驱动程序可以使用[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))并[ **KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)来获取和释放作为数值调节钮锁*排队自旋锁*。 排队的自旋锁在多处理器计算机上提供更好的性能比普通数值调节钮的大量争用锁的锁。 有关详细信息，请参阅[排队旋转锁](queued-spin-locks.md)。 适用于 Windows 2000 的驱动程序可以使用[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)并[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)来获取和发布为普通的旋转锁自旋锁。

若要同步对简单的数据结构的访问，驱动程序可以使用任一**ExInterlocked * Xxx*** 例程以确保数据结构的原子访问。 使用这些例程的驱动程序不需要以获取或者显式释放自旋锁。

具有 ISR 每个驱动程序将使用*中断自旋锁*若要保护的任何数据或其 ISR 之间共享的硬件并将其[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)通常是例程从调用其[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)并[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程。 中断自旋锁是与中断时该驱动程序调用创建的对象组相关联[ **IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)，如下所述注册 ISR.

**请遵循以下准则，以便在驱动程序中使用自旋锁：**

-   为任何数据或保护旋转锁的资源以及在内存中驻留的系统空间的相应数值调节钮锁提供存储 (非分页缓冲的池，如中所示[虚拟内存空间和物理内存](overview-of-windows-memory-space.md)图)。 它使用任何 executive 自旋锁，驱动程序必须提供存储。 但是，设备驱动程序无需提供存储用于中断自旋锁除非 multivector ISR 或者具有多个 ISR 注册 ISR.中所述

-   调用[ **KeInitializeSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)初始化为其驱动程序提供存储然后使用它来同步对共享的数据或其保护的资源的访问每个旋转锁。

-   调用使用旋转锁在适当的 IRQL，通常在每个支持例程&lt;= 调度\_executive 自旋锁或在级别&lt;= DIRQL 与驱动程序的中断对象相关联的中断自旋锁。

-   实现例程，从而尽可能快地执行，而它们持有自旋锁。 没有例程应保存旋转锁的时间超过 25 微秒为单位。

-   永远不会实施执行同时保留数值调节钮锁定以下任意操作的例程：

    -   会导致硬件异常或引发软件异常。

    -   尝试访问可分页内存。

    -   品牌的递归调用，将导致死锁或可能导致旋转锁保留时间超过 25 微秒为单位。

    -   尝试获取另一个旋转锁，如果这样做可能会导致死锁。

    -   调用违反了任何上述规则的外部例程。

 

 




