---
title: 信号量对象
description: 信号量对象
ms.assetid: e6703c39-3b47-4d3b-86e7-bf2bf37af493
keywords:
- 内核调度程序对象 WDK，信号量对象
- 调度程序对象 WDK 内核，信号量对象
- 信号量对象 WDK 内核
- KeInitializeSemaphore
- 正在等待信号量对象
- KeReleaseSemaphore
- 计数信号量 WDK 内核
- 二进制信号量 WDK 内核
- 等待状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d512786419ff1104986e9a8d2fe080a11f6dff6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542933"
---
# <a name="semaphore-objects"></a>信号量对象





任何驱动程序可以使用信号量对象来同步其驱动程序创建的线程和其他驱动程序例程之间的操作。 例如，驱动程序专用的线程可能会将自身置于等待状态时驱动程序，没有未完成 I/O 请求和驱动程序的调度例程可能会将信号灯设置为用信号通知状态只是它们排队 IRP 后。

请求的 I/O 操作的线程的上下文中运行的最高级别的驱动程序的调度例程可能会使用一个信号量来保护的调度例程之间共享的资源。 同步 I/O 操作的较低级驱动程序调度例程也可能使用信号量来保护或与驱动程序创建线程的调度例程的子集之间共享的资源。

使用信号量对象的任何驱动程序必须调用[ **KeInitializeSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff552150)它等待或释放信号量之前。 下图说明了如何使用线程的驱动程序可以使用信号量对象。

![说明等待信号量对象的关系图](images/3semobj.png)

上图所示，这样的驱动程序必须为信号量对象，它应该是常驻提供存储。 可以使用该驱动程序[设备扩展](device-extensions.md)的驱动程序创建的设备对象，如果它使用的控制器扩展[控制器对象](using-controller-objects.md)，或由驱动程序分配的非分页缓冲的池。

当驱动程序的[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程调用**KeInitializeSemaphore**，它必须将一个指针传递给驱动程序的信号量对象的常驻存储。 此外，调用方必须指定*计数*信号量对象，如在上图所示，它确定其初始状态 （用信号通知为非零）。

调用方还必须指定*限制*的信号量，可以是以下之一：

-   **限制 = 1**

    当此信号量设置为用信号通知状态时，单个线程等待信号量可重置为未用信号通知状态变得符合条件执行，并且可以访问任何资源进行保护的信号量。

    这种类型的信号量也称为*二进制的 semaphore*因为线程具有或不具有到信号量受保护资源的独占访问权限。

-   **限制&gt;1**

    当此信号量设置为用信号通知状态时，一定数量的线程在等待信号量对象设置为未用信号通知能够执行和状态可以访问任何资源进行保护的信号量。

    此类型的信号量称为*计数信号量*因为将信号量设置为用信号通知状态的例程还指定了多少个等待线程可以具有其状态更改从等待变为就绪。 此类正在等待的线程数可为*限制*集初始化信号量时或一定数量小于此预设*限制*。

几个设备或中间驱动程序有一个驱动程序创建线程;甚至更少具有一组可能会等待信号量以获取或释放的线程。 几个系统提供的驱动程序将信号量对象，和的那些确实，甚至更少使用二进制的 semaphore。 尽管一个二进制的 semaphore 可能看起来是在功能上类似[mutex 对象](mutex-objects.md)，一个二进制的 semaphore 不提供内置保护功能的互斥体对象已在 SMP 计算机中运行的系统线程的死锁。

加载的驱动程序有初始化的信号量后，它可以同步对保护共享的资源的信号量的操作。 例如，驱动程序与设备专用线程，用于管理系统软盘控制器驱动程序，如队列 Irp，可能会同步 IRP 队列上一个信号量，在上图中所示：

1.  该线程在调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)用一个指针指向要将自身置于等待状态的已初始化的信号量对象的驱动程序提供存储。

2.  Irp 开始进入需要设备 I/O 操作。 驱动程序的调度例程下数值调节钮锁定控件，并调用互锁队列中插入每个此类 IRP [ **KeReleaseSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff553143)用一个指针指向驱动程序确定的信号量对象线程优先级提升 (*增量*，如在上图中所示)、 一个*调整*1 添加到的信号量计数为排队每个 IRP 和一个布尔值的*等待*设置为**FALSE**。 非零值的信号量计数设置为用信号通知状态，从而更改正在等待线程的状态变为就绪信号量对象。

3.  内核为处理器可调度线程中的执行： 即，具有较高优先级没有其他线程当前处于就绪状态和有要在更高版本的 IRQL 运行没有内核模式例程。

    该线程从互锁下旋转锁控制队列中移除 IRP，将其传递到其他驱动程序例程进行进一步处理，并调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)试。 如果信号量仍设置为用信号通知状态 （即，其计数保持为非零值，指示多个 Irp 处于互锁队列中的驱动程序），为就绪情况下内核再次从等待更改线程的状态。

    通过以这种方式使用计数信号量，此类驱动程序线程"知道"没有 IRP 要每当运行该线程从互锁的队列中删除。

调用[ **KeReleaseSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff553143)与*等待*参数设置为**TRUE**指示调用方的意图立即调用**KeWait*Xxx*对象**(s) 支持例程返回时从**KeReleaseSemaphore**。

请考虑下面的设置的指导*等待*KeReleaseSemaphore 参数：

可分页的线程或在被动 IRQL 运行的可分页的驱动程序例程\_级别应永远不会调用**KeReleaseSemaphore**与*等待*参数设置为**TRUE**. 此类调用会导致严重的页面错误，如果调用方碰巧换出到调用之间**KeReleaseSemaphore**并**KeWait*Xxx*对象**(s)。

在晚于被动的 IRQL 运行任何标准驱动程序例程\_级别不能等待非零值的时间间隔上的所有调度程序对象而不会降低系统停止; 请参阅[内核调度程序对象](kernel-dispatcher-objects.md)有关详细信息。 但是，可以调用此类例程**KeReleaseSemaphore**调度的 IRQL 小于或等于在运行时\_级别。

在运行的标准驱动程序例程于 Irql 的摘要，请参阅[管理硬件优先级](managing-hardware-priorities.md)。 特定的 IRQL 要求支持例程，请参阅例程的参考页。

 

 




