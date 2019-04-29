---
title: 使用计时器对象
description: 使用计时器对象
ms.assetid: b3ee9d92-87b9-47b7-ab13-11e42bec7997
keywords:
- 计时器对象 WDK 内核等待
- 等待计时器对象
- 通知计时器 WDK 内核
- KeDelayExecutionThread
- KeWaitForSingleObject
- KeInitializeTimer
- KeSetTimer
- DueTime 值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f90310aa08bd9780a70f619c998a93f72ee2c57f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372198"
---
# <a name="using-timer-objects"></a>使用计时器对象





下图说明了使用设置操作的超时间隔和其他驱动程序例程处理 I/O 请求，并等待通知计时器。

![说明等待计时器对象的关系图](images/3ketimer.png)

上图所示，驱动程序必须提供存储计时器对象，必须通过调用初始化[ **KeInitializeTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff552168)用一个指针指向此存储。 驱动程序，通常可以从此调用其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。

驱动程序创建线程或线程请求同步 I/O 操作，例如在特定线程的上下文中该驱动程序可以等待其计时器对象上图中所示：

1.  该线程在调用[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)用一个指针指向计时器对象和一个给定*DueTime*的 100 纳秒为单位表示的值。 一个正值*DueTime*指定一个绝对时间计时器对象应是从内核的计时器队列中删除且将设置为用信号通知状态。 负值*DueTime*指定相对于当前系统时间间隔。

    请注意，线程 （或驱动程序在系统线程中的例程正在运行） 将传递**NULL** DPC 对象的指针 (在图演示前面所示[CustomTimerDpc 例程使用计时器和DPC对象](registering-and-queuing-a-customtimerdpc-routine.md))当调用**KeSetTimer**如果等待计时器对象而不是队列[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程。

2.  该线程在调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)与指向计时器对象的指针，这是将放在线程置于等待状态内核的计时器队列中的计时器对象时。

3.  给定*DueTime*过期。

4.  内核取消排队的计时器对象，将其设置为用信号通知状态，并从等待线程的状态更改为就绪。

5.  内核为处理器可调度线程中的执行： 即，具有较高优先级没有其他线程当前处于就绪状态和有要在更高版本的 IRQL 运行没有内核模式例程。

在 IRQL 运行的驱动程序例程&gt;= 调度\_级别可以使用计时器对象相关联的 DPC 对象排队驱动程序提供的超时请求[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程。 Nonarbitrary 线程上下文中运行的驱动程序例程上可等待非零间隔计时器对象，如在上图中所示。

每个其他线程，如驱动程序创建的线程由内核线程对象，也是一个调度程序对象表示。 因此，驱动程序不需要使用计时器对象要自愿将本身置于等待状态的给定间隔其驱动程序创建线程。 相反，线程可以调用[ **KeDelayExecutionThread** ](https://msdn.microsoft.com/library/windows/hardware/ff551986)与调用方提供的时间间隔。 有关此技术的详细信息，请参阅[轮询设备](avoid-polling-devices.md)。

[**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)， [*重新初始化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)，以及[*卸载*](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程也在系统线程中运行上下文，因此驱动程序可以调用**KeWaitForSingleObject**与驱动程序初始化计时器对象或**KeDelayExecutionThread**而正在初始化或卸载它们。 设备驱动程序可以调用[ **KeStallExecutionProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff553295)很短的间隔 （最好是一个少于 50 微秒为单位） 如果要在其初始化过程中更新状态的设备必须等到.

但是，更高级别的驱动程序通常使用中的另一个同步机制及其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)并[*重新初始化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)而不是使用计时器对象的例程。 更高级别的驱动程序始终应设计为通过特定类型或类型的设备的任何较低级别驱动程序层本身。 因此，更高级别的驱动程序往往会变慢加载它等待计时器对象或调用**KeDelayExecutionThread**因为这样的驱动程序必须等待一段时间足够长的时间以适应最慢的可能的设备支持它。 另请注意，此类等待"安全"，但最小时间间隔是很难确定。

同样，即插即用驱动程序不必等待其他操作发生，而是应使用的即插即用管理器[通知](using-pnp-notification.md)机制。

 

 




