---
title: 自旋锁简介
description: 自旋锁简介
ms.assetid: a37c0db4-ff9c-4958-a9f4-62b671458d03
keywords:
- KSPIN_LOCK
- executive 旋转锁定 WDK 内核
- 中断自旋锁定 WDK 内核
- 排队自旋锁 WDK 内核
- 旋转锁定 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 963bc0811925ce8eb4fc28bb02c421e3563002e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838622"
---
# <a name="introduction-to-spin-locks"></a>自旋锁简介





自旋锁是内核定义的仅限内核模式的同步机制，作为不透明类型导出： KSPIN\_锁定。 自旋锁可用于保护共享数据或资源，使其能够以并发方式并行访问，同时可在 SMP 计算机上 &gt;= 调度\_级别并发执行。

许多组件使用自旋锁（包括驱动程序）。 任何类型的驱动程序都可以使用一个或多个*执行自旋锁*。 例如，大多数文件系统在文件系统驱动程序的（FSD）设备扩展中使用联锁工作队列来存储由文件系统的工作线程回调例程和 FSD 处理的 Irp。 联锁工作队列受 executive 旋转锁保护，该锁可解决 FSD 中尝试将 Irp 插入队列的争用，以及同时尝试删除 Irp 的所有线程。 作为另一个示例，系统软盘控制器驱动程序使用两个执行自旋锁。 一个 executive 旋转锁可保护与此驱动程序的设备专用线程共享的联锁工作队列;另一种方法是保护由三个驱动程序例程共享的计时器对象。

适用于 Microsoft Windows XP 和更高版本 Windows 的驱动程序可以使用[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))和[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)获取并释放作为*排队旋转锁*的旋转锁。 对于多处理器计算机上的高争用锁，排队自旋锁比普通旋转锁提供更好的性能。 有关详细信息，请参阅[排队自旋锁](queued-spin-locks.md)。 适用于 Windows 2000 的驱动程序可以使用[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)和[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)获取并释放旋转锁定作为普通旋转锁。

为了同步访问简单的数据结构，驱动程序可以使用任何**ExInterlocked * Xxx*** 例程来确保对数据结构的原子访问。 使用这些例程的驱动程序无需显式获取或释放旋转锁。

具有 ISR 的每个驱动程序都使用*中断自旋锁*来保护其 ISR 与其[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程之间共享的任何数据或硬件，这些例程通常从其[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)和[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程调用。 中断自旋锁与驱动程序调用[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)时创建的中断对象集相关联，如注册 ISR 中所述。

**请按照以下准则来使用驱动程序中的自旋锁：**

-   为由自旋锁保护的任何数据或资源提供存储，并为常驻系统空间内存（非分页池，如[虚拟内存空间和物理内存](overview-of-windows-memory-space.md)图中所示）中的相应旋转锁提供存储。 驱动程序必须为其使用的任何执行自旋锁提供存储空间。 但是，设备驱动程序无需为中断旋转锁定提供存储，除非它具有 multivector ISR 或具有多个 ISR，如注册 ISR 中所述。

-   调用[**KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock) ，初始化驱动程序为其提供存储的每个自旋锁，然后使用它来同步访问它所保护的共享数据或资源。

-   调用每个支持例程，该例程在适当的 IRQL 处使用自旋锁，一般为：对于执行自旋锁，则为 &lt;= 调度\_级别; 对于与驱动程序中断对象关联的中断自旋锁，则为 &lt;= DIRQL。

-   在持有自旋锁的情况下，尽可能快地执行例程来执行。 任何例程都不应将旋转锁定保留超过25微秒。

-   在持有自旋锁的情况下，切勿实现执行以下任一操作的例程：

    -   导致硬件异常或引发软件异常。

    -   尝试访问可分页内存。

    -   发出一个递归调用，该调用会导致死锁，或导致保持旋转锁的时间超过25微秒。

    -   如果执行此操作可能会导致死锁，则尝试获取另一个自旋锁。

    -   调用与上述任何规则冲突的外部例程。

 

 




