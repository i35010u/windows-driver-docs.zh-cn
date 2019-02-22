---
title: 同步和网络驱动程序中的通知
description: 同步和网络驱动程序中的通知
ms.assetid: 9fd9306f-5431-485f-9d6b-f7d6f25ea1ce
keywords:
- 同步对 WDK 网络资源的访问
- 同步 WDK 网络
- 通知 WDK 网络
- 数值调节钮锁定 WDK 网络
- 网络驱动程序 WDK，通知有关事件的驱动程序
- 通知有关事件 WDK 网络驱动程序
- 共享的资源 WDL 网络
- 计时器 WDK 网络
- 事件通知 WDK 网络
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419fb53f0e53eecb6441c148ad975dcb70622c32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547425"
---
# <a name="synchronization-and-notification-in-network-drivers"></a>同步和网络驱动程序中的通知





只要两个执行线程共享资源可在同一时间，在单处理器计算机中或在对称多处理器 (SMP) 计算机上访问他们需要进行同步。 例如，在单处理器计算机中，如果一个驱动程序函数访问共享的资源，并在更高版本的 IRQL，如 ISR 运行的另一个函数被中断的共享的资源必须受到保护，以防保留中的资源的争用条件不确定状态。 在 SMP 计算机上，两个线程是不同的处理器上运行的同时，尝试修改相同的数据。 必须在同步此类访问。

NDIS 提供了可用于同步在相同的 IRQL 运行的线程之间共享资源的访问权限的自旋锁。 当在不同于 Irql 运行共享资源的两个线程时，NDIS 提供用于暂时引发较低的 IRQL 代码的 IRQL，以便访问共享资源的权限可序列化的机制。

当一个线程依赖于线程之外的事件的匹配项时，该线程依赖于通知。 例如，驱动程序可能需要一些时间段已过去，以便它可以检查其设备时收到通知。 或网络接口卡 (NIC) 驱动程序可能需要执行如轮询的定期操作。 计时器提供这样一种机制。

事件提供一种机制，可以使用两个执行线程同步操作。 例如，微型端口驱动程序可以通过写入设备测试 NIC 上的中断。 该驱动程序必须等待中断通知驱动程序操作已成功。 事件可用于同步完成的中断正在等待的线程和处理中断的线程之间的操作。

本主题中的以下各个小节介绍了这些 NDIS 机制。

-   [自旋锁](#spin-locks)
-   [避免数值调节钮锁定问题](#avoiding-spin-lock-problems)
-   [计时器](#timers)
-   [事件](#events)

### <a name="spin-locks"></a>自旋锁

一个*旋转锁*提供了用于保护共享的内核模式线程在 IRQL 运行资源的同步机制&gt;被动\_级别在单处理器或多处理器计算机中。 旋转锁处理各种线程间同步的 SMP 计算机同时运行的执行。 一个线程访问受保护的资源之前获取自旋锁。 旋转锁保留一个持有自旋锁从使用资源的任何线程。 SMP 计算机上，线程正在等待自旋锁循环尝试获取自旋锁释放的线程前，持有锁。

自旋锁的另一个特征是相关联的 IRQL。 尝试的获取的自旋锁暂时引发 IRQL 与旋转锁关联到请求线程的 IRQL。 这可以防止在同一处理器上的所有较低的 IRQL 线程优先执行的线程。 在更高版本的 IRQL 运行在同一处理器上的线程可抢占执行线程，但这些线程无法获取数值调节钮锁，因为它具有较低的 IRQL。 因此，一个线程已获取了自旋锁后，没有其他线程可以获取，直到已释放自旋锁。 编写良好的网络驱动程序最小化自旋锁的时间量。

旋转锁的典型用法是保护队列。 例如，微型端口驱动程序将发送函数， [ *MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)，可能会传递给它的协议驱动程序的数据包进行排队。 其他驱动程序函数还使用此队列中，因为*MiniportSendNetBufferLists*必须保护旋转锁的队列，以便一次只有一个线程可以操作的链接或内容。 *MiniportSendNetBufferLists*获取数值调节钮锁将数据包添加到队列，然后释放自旋锁。 使用旋转锁可确保持有锁的线程是安全地将数据包添加到队列时修改队列链接的唯一线程。 从队列数据包微型端口驱动程序时，此类访问受相同的旋转锁。 运行时修改的队列或任何链接字段组成队列开头的说明，该驱动程序必须保护旋转锁的队列。

驱动程序必须注意不要过度保护队列。 例如，驱动程序可以执行某些操作 （例如，在包含长度的字段中填充） 数据包的网络驱动程序保留字段中之前队列数据包。 驱动程序可以执行此操作由数值调节钮锁保护的代码区域外，但必须在队列数据包之前执行。 数据包是在队列上并正在运行的线程释放自旋锁后，该驱动程序必须假定其他线程可以取消立即排队数据包。

### <a name="avoiding-spin-lock-problems"></a>避免数值调节钮锁定问题

若要避免可能的死锁，NDIS 驱动程序应释放所有 NDIS 自旋锁而不调用 NDIS 函数之前**Ndis*Xxx*旋转锁**函数。 如果 NDIS 驱动程序不符合此要求，则会按如下所示发生死锁：

1. 线程 1，其中包含 NDIS 自旋锁的调用**Ndis * Xxx*** 函数尝试获取 NDIS 通过调用旋转锁 B [ **NdisAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff560699)函数。

2. 线程 2，它保存 NDIS 自旋锁 B，调用**Ndis * Xxx*** 尝试通过调用获取 NDIS 自旋锁的函数**NdisAcquireSpinLock**函数。

3. 线程 1 和线程 2 中，每个正在等待其他释放自旋锁，会发生死锁。

Microsoft Windows 操作系统不会限制网络驱动程序同时持有多个数值调节钮锁。 但是，如果一个部分中的驱动程序尝试获取数值调节钮锁定一个存放自旋锁 B，而另一个部分尝试按住自旋锁的同时获取数值调节钮锁 B 时，死锁的结果。 如果它获取多个数值调节钮锁时，驱动程序应通过强制实施的采购订单避免死锁。 也就是说，如果驱动程序强制实施获取数值调节钮锁 A 之前自旋锁 B，上面所述的情况不会发生。

获取数值调节钮锁引发调度到 IRQL\_级别和存储旋转锁中的旧 IRQL。 释放自旋锁将 IRQL 设置为旋转锁中存储的值。 因为 NDIS 有时进入驱动程序在被动\_级别，可能会出现问题与下面的代码序列：

```syntax
NdisAcquireSpinLock(A);
NdisAcquireSpinLock(B);
NdisReleaseSpinLock(A);
NdisReleaseSpinLock(B);
```

驱动程序不应访问此序列中的自旋锁，原因如下：

-   释放自旋锁 A 和释放数值调节钮之间锁定 B，代码运行在被动\_级别而不是调度\_级别，并且受到不适当的中断。

-   在释放数值调节钮后锁定 B，请在代码运行在调度\_级别，这可能会导致调用方的错误，在得更高版本时使用的 IRQL\_不\_较少\_或\_相等停止错误。

使用自旋锁会影响性能，并且一般情况下，驱动程序不应使用许多自旋锁。 有时，通常是非重复的函数 （例如，发送和接收函数） 具有次要的两个数字显示为可以使用锁的重叠。 使用多个数值调节钮锁以允许独立运行在不同处理器的两个函数可能物有所值之间取得平衡。

### <a name="timers"></a>计时器

计时器用于轮询或导致操作超时。 驱动程序创建一个计时器，并将函数与计时器相关联。 如果在计时器中指定的期限过期时调用相关联的函数。 计时器可以单步或定期。 一旦设置定期计时器，它将继续，直到显式清除每个期限过期时引发。 每次它引发时，都必须重置单步计时器。

创建和初始化通过调用计时器[ **NdisAllocateTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561618)并通过调用设置[ **NdisSetTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff564563)。 如果使用非周期性的计时器，则它必须通过调用重置**NdisSetTimerObject**。 通过调用清除计时器[ **NdisCancelTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561624)。

### <a name="events"></a>事件

事件用于同步两个执行线程之间的操作。 事件是由驱动程序分配，并通过调用来初始化[ **NdisInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562732)。 在 IRQL 运行的线程 = 被动\_级别调用[ **NdisWaitEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff564651)本身置于等待状态。 驱动程序线程等待事件，它指定要等待的最长时间，以及要等待的事件。 线程的等待是满足[ **NdisSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff564539)是调用导致事件发出信号，或指定的最大等待时间间隔过期时，以先发生者为准。

通常情况下，将事件设置调用的协作线程**NdisSetEvent**。 在创建和必须设置以便向等待线程发出信号时，事件是信号。 事件保持终止状态，直到[ **NdisResetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff564526)调用。

## <a name="related-topics"></a>相关主题


[网络驱动程序中的多处理器支持](multiprocessor-support-in-network-drivers.md)

 

 






