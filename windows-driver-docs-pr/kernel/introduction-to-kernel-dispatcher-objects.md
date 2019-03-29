---
title: 内核调度程序对象简介
description: 内核调度程序对象简介
ms.assetid: acf7b19a-55a3-4d9b-87ff-ca4df9ed3a45
keywords:
- 内核调度程序对象 WDK，关于内核调度程序对象
- 调度程序对象 WDK 内核，有关内核调度程序对象
- 等待状态 WDK 内核
- 已发出信号的状态 WDK 内核
- 不发出信号状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53a6530955b26e9da466c813312d67cd65d3e0c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562751"
---
# <a name="introduction-to-kernel-dispatcher-objects"></a>内核调度程序对象简介





内核定义一组的对象类型称为*内核调度程序对象*，或仅*调度程序对象*。 调度程序对象包括计时器对象、 事件对象、 信号量对象、 互斥体对象和线程对象。

驱动程序可以使用调度程序对象作为 nonarbitrary 线程上下文中的同步机制在 IRQL 被动执行时\_级别。

### <a name="dispatcher-object-states"></a>调度程序对象状态

每个内核定义调度程序对象类型具有设置到用信号通知，或者设置为未用信号通知的状态。

一组线程可以同步其操作，如果一个或多个线程调用[ **KeWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff553350)， [ **KeWaitForMutexObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553344)，或[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)。 这些函数采用调度程序对象指针作为输入并等待，直到另一个例程或线程将一个或多个调度程序对象设置为用信号通知状态。

当线程调用**KeWaitForSingleObject**等待调度程序对象 (或**KeWaitForMutexObject**互斥体)，该线程放入*等待*状态直到调度程序对象设置为用信号通知状态。 一个线程可以调用**KeWaitForMultipleObjects**等待任何操作，或所有，调度程序对象是一组设置为用信号通知。

内核时调度程序对象设置为用信号通知状态，更改该对象正在等待任何线程的状态*准备*。 （同步计时器和同步事件都是此规则的例外情况; 只有一个等待线程时同步事件或计时器发出信号，设置为就绪状态。 有关详细信息，请参阅[计时器对象和 dpc 进行标记](timer-objects-and-dpcs.md)并[事件对象](event-objects.md)。)处于就绪状态的线程将按计划运行根据其当前的运行时[线程优先级](thread-priorities.md)和任何具有该优先级的线程的处理器的当前可用性。

### <a name="when-can-drivers-wait-for-dispatcher-objects"></a>何时可以驱动程序等待调度程序对象？

一般情况下，驱动程序可以等待调度程序对象来设置仅当至少一个在以下情况下为 true:

-   Nonarbitrary 线程上下文中执行时，驱动程序。

    也就是说，您可以标识将进入等待状态的线程。 在实践中，是 nonarbitrary 线程上下文中执行的唯一驱动程序例程[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)， [ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)， [*重新初始化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)，和[*卸载*](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程的任何驱动程序，以及最高级别的驱动程序的调度例程。 所有这些例程直接由系统调用。

-   该驱动程序正在执行完全同步 I/O 请求。

    即，没有驱动程序队列的任何操作时处理 I/O 请求，并且未驱动程序返回，直到其下的驱动程序已完成处理请求。

此外，驱动程序不能进入等待状态，如果在执行或上面 IRQL = 调度\_级别。

由于这些限制，必须使用以下规则：

-   **DriverEntry**， *AddDevice*，*重新初始化*，以及*卸载*例程的任何驱动程序可以等待调度程序对象。

-   最高级别的驱动程序的调度例程可以等待调度程序对象。

-   调度例程的较低级驱动程序可以等待调度的对象，如果 I/O 操作是同步、，例如创建、 刷新，请关闭，并关闭操作、 某些设备 I/O 控制操作，以及一些 PnP 和电源操作。

-   较低级别的驱动程序的调度例程不能等待异步 I/O 操作完成的调度程序对象。

-   在或更高版本的 IRQL 调度正在执行的驱动程序例程\_级别必须等待要设置为用信号通知状态的调度程序对象。

-   驱动程序必须尝试等待要设置为用信号通知状态为完成的传输操作中到或从分页设备的调度程序对象。

-   驱动程序调度例程维护读/写请求通常不能等待要设置为用信号通知状态的调度程序对象。

-   设备 I/O 控制请求的调度例程可以等待调度程序对象设置为用信号通知状态才传输类型的 I/O 控制代码是方法\_缓冲。

-   SCSI 微型端口驱动程序不应使用内核调度程序对象。 SCSI 微型端口驱动程序应只调用[SCSI 端口库例程](https://msdn.microsoft.com/library/windows/hardware/ff565375)。

在任意线程上下文中执行其他每个标准驱动程序例程： 的任何线程恰巧是当前用于处理排队的操作或用于处理设备中断调用驱动程序例程。 此外，在引发 IRQL，在调度运行大多数标准驱动程序例程\_级别，或设备驱动程序，请在 DIRQL。

如果有必要，驱动程序可以创建设备专用线程，这可以等待该驱动程序的其他例程 (除非 ISR 或[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程) 将调度程序对象设置为用信号通知状态和重置为未发出信号状态。

一般原则是，如果希望在新的设备驱动程序将通常需要在 I/O 操作期间等待设备状态更改时停止的时间超过 50 微秒，考虑实施的驱动程序与设备专用线程。 如果设备驱动程序也是最高级别的驱动程序，请考虑使用[系统工作线程数](system-worker-threads.md)和实现一个或多个工作线程回调例程。 请参阅[ **PsCreateSystemThread** ](https://msdn.microsoft.com/library/windows/hardware/ff559932)并[管理与驱动程序创建线程的联锁的队列](managing-interlocked-queues-with-a-driver-created-thread.md)。

 

 




