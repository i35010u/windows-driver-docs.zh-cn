---
title: 网络驱动程序中的同步和通知
description: 网络驱动程序中的同步和通知
ms.assetid: 9fd9306f-5431-485f-9d6b-f7d6f25ea1ce
keywords:
- 同步访问资源 WDK 网络
- 同步 WDK 网络
- 通知 WDK 网络
- 旋转锁定 WDK 网络
- 网络驱动程序 WDK，通知驱动程序事件
- 通知驱动程序事件 WDK 网络
- 共享资源 WDL 网络
- 计时器的 WDK 网络
- 事件通知 WDK 网络
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfc84fd72ac9a12982397aaef54d63135394f6b5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207159"
---
# <a name="synchronization-and-notification-in-network-drivers"></a>网络驱动程序中的同步和通知





只要两个执行线程共享可同时访问的资源，无论是在单处理器计算机上，还是在 (SMP) 计算机的对称多处理器上，它们都需要同步。 例如，在单处理器计算机上，如果一个驱动程序函数正在访问共享资源，并且被另一个运行的函数（如 ISR）中断，则必须对共享资源进行保护，以防止出现使资源处于不确定状态的争用情况。 在 SMP 计算机上，两个线程可以同时在不同的处理器上运行，并尝试修改相同的数据。 必须同步此类访问。

NDIS 提供了自旋锁，可用于同步对在相同 IRQL 上运行的线程之间的共享资源的访问。 当共享资源的两个线程在不同的 IRQLs 上运行时，NDIS 会提供一种机制来暂时引发较低 IRQL 代码的 IRQL，以便能够序列化对共享资源的访问。

当线程依赖于线程外发生的事件时，该线程依赖于通知。 例如，可能需要在某些时间段过后通知驱动程序，以便可以检查其设备。 或网络接口卡 (NIC) 驱动程序可能需要执行定期操作，如轮询。 计时器提供此类机制。

事件提供了两个执行线程可用于同步操作的机制。 例如，微型端口驱动程序可以通过写入设备来测试 NIC 上的中断。 驱动程序必须等待中断，通知驱动程序操作成功。 您可以使用事件在等待中断的线程和处理中断的线程之间同步操作。

本主题中的以下小节介绍了这些 NDIS 机制。

-   [自旋锁](#spin-locks)
-   [避免旋转锁定问题](#avoiding-spin-lock-problems)
-   [计时器](#timers)
-   [事件](#events)

### <a name="spin-locks"></a>自旋锁

*旋转锁*提供一种同步机制，用于保护在 &gt; 单处理器 \_ 计算机或多处理器计算机上运行的内核模式线程所共享的资源。 自旋锁处理在 SMP 计算机上并发运行的各种执行线程之间的同步。 在访问受保护的资源之前，线程将获取自旋锁。 旋转锁定会保留任何线程，但包含自旋锁的线程使用资源。 在 SMP 计算机上，等待旋转锁定的线程会循环尝试获取旋转锁，直到持有锁的线程释放它。

自旋锁的另一特性是关联的 IRQL。 尝试获取旋转锁将暂时引发请求线程的 IRQL 与自旋锁关联的 IRQL。 这可以防止同一处理器上的所有较低 IRQL 线程抢占执行线程。 在同一处理器上，以更高的 IRQL 运行的线程可以抢占正在执行的线程，但这些线程无法获取自旋锁，因为它的 IRQL 较低。 因此，在线程获取旋转锁后，任何其他线程都无法获取旋转锁定，直到它被释放。 编写良好的网络驱动程序可最大程度地缩短旋转锁的保留时间。

旋转锁的典型用途是保护队列。 例如，微型端口驱动程序 send 函数 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)可能会通过协议驱动程序将传递给它的数据包排队。 由于其他驱动程序函数也使用此队列，因此 *MiniportSendNetBufferLists* 必须使用自旋锁保护队列，以便一次只有一个线程可以操作链接或内容。 *MiniportSendNetBufferLists* 获取旋转锁，将数据包添加到队列中，然后释放旋转锁。 使用自旋锁可以确保持有锁的线程是在安全地将数据包添加到队列时修改队列链接的唯一线程。 当微型端口驱动程序将数据包从队列中取出时，此类访问将受到相同的自旋锁保护。 当运行说明来修改队列的头或构成队列的任何链接字段时，驱动程序必须使用旋转锁来保护队列。

驱动程序必须注意不 overprotect 队列。 例如，驱动程序可以执行某些操作 (例如，在将数据包排队之前填写包含数据包的 "网络驱动程序保留" 字段中的长度) 字段。 驱动程序可以在由自旋锁保护的代码区域外执行此操作，但必须在排队数据包之前执行此操作。 当数据包在队列上并且正在运行的线程释放旋转锁时，驱动程序必须假定其他线程可以立即取消包的排队。

### <a name="avoiding-spin-lock-problems"></a>避免旋转锁定问题

若要避免可能出现的死锁，NDIS 驱动程序应在调用 ndis ***Xxx*旋转锁**函数之外的其他 ndis 函数之前释放所有 NDIS 自旋锁。 如果 NDIS 驱动程序不符合此要求，则会发生死锁，如下所示：

1. 线程1（其中包含 NDIS 自旋锁 A）调用 **ndis * Xxx*** 函数，该函数尝试通过调用 [**NDISACQUIRESPINLOCK**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock) 函数获取 ndis 自旋锁 B。

2. 线程2（包含 NDIS 自旋锁 B）调用 **ndis * Xxx*** 函数，该函数尝试通过调用 **NDISACQUIRESPINLOCK** 函数获取 ndis 自旋锁 A。

3. 线程1和线程2，每个线程都在等待另一个线程释放其旋转锁。

Microsoft Windows 操作系统不会限制网络驱动程序同时保留多个自旋锁。 但是，如果驱动程序的一个部分尝试获取旋转锁 A，同时持有旋转锁 B，而另一个节尝试获取旋转锁 B，同时持有自旋锁 A，会导致死锁结果。 如果它获取了多个旋转锁，则驱动程序应通过强制实现顺序来避免死锁。 也就是说，如果驱动程序在旋转锁 B 之前强制获取自旋锁 A，则不会发生上述情况。

获取旋转锁会将 IRQL 提高到调度 \_ 级别，并将旧的 IRQL 存储在旋转锁定中。 释放自旋锁会将 IRQL 设置为存储在旋转锁中的值。 由于 NDIS 有时会在被动级别进入驱动程序 \_ ，因此可能会出现以下代码序列的问题：

```syntax
NdisAcquireSpinLock(A);
NdisAcquireSpinLock(B);
NdisReleaseSpinLock(A);
NdisReleaseSpinLock(B);
```

由于以下原因，驱动程序不应访问此序列中的自旋锁：

-   在释放自旋锁 A 和释放旋转锁 B 之间，代码在被动 \_ 级别（而不是调度级别）运行， \_ 并且受到不当中断的影响。

-   释放旋转锁 B 后，代码在调度级别运行， \_ 这可能会导致调用方在更晚时间出现错误，并且 IRQL \_ 不 \_ 小于 \_ 或 \_ 等于停止错误。

使用自旋锁会影响性能，通常情况下，驱动程序不应使用多个自旋锁。 有时，通常是不同的函数 (例如，send 和 receive 函数) 有次重叠，可以使用两个自旋锁。 如果使用多个自旋锁，则可能会有一定的折衷，使这两个函数在单独的处理器上独立运行。

### <a name="timers"></a>计时器

计时器用于轮询或超时操作。 驱动程序将创建一个计时器，并将函数与计时器相关联。 当计时器中指定的时间段过期时，将调用关联的函数。 计时器可以是一步，也可以是周期性的。 一旦设置了定期计时器，它将在每个时间段的过期时间继续触发，直到显式清除。 每次激发时，必须重置一个单步计时器。

计时器是通过调用 [**NdisAllocateTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject) 来创建和初始化的，并通过调用 [**NdisSetTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)进行设置。 如果使用非周期性计时器，则必须通过调用 **NdisSetTimerObject**进行重置。 通过调用 [**NdisCancelTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)清除计时器。

### <a name="events"></a>事件

事件用于在两个执行线程之间同步操作。 事件由驱动程序分配，并通过调用 [**NdisInitializeEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent)进行初始化。 以 IRQL = 被动级别运行的线程 \_ 将调用 [**NdisWaitEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent) ，以将其本身置于等待状态。 当驱动程序线程等待某个事件时，它将指定等待的最长时间以及要等待的事件。 调用 [**NdisSetEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetevent) 时，如果调用了导致事件发出信号的事件或指定的最长等待时间间隔到期（以先发生者为准），则满足线程的等待。

通常情况下，事件由调用 **NdisSetEvent**的协作线程设置。 在创建事件时信号事件，必须将其设置为等待线程的信号。 在调用 [**NdisResetEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisresetevent) 之前，事件会一直保持终止状态。

## <a name="related-topics"></a>相关主题


[网络驱动程序中的多处理器支持](multiprocessor-support-in-network-drivers.md)

 

