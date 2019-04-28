---
title: 互斥对象简介
description: 互斥对象简介
ms.assetid: c35b4341-09dd-411d-b933-6c762fecd23c
keywords:
- 内核调度程序对象 WDK，互斥体对象
- 调度程序对象 WDK 内核，互斥体对象
- 互斥体对象 WDK 内核
- 互斥独占访问 WDK 内核
- 等待 mutex 对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff495e947018a6689b4e85e75f8518e5d3710d5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341452"
---
# <a name="introduction-to-mutex-objects"></a>互斥对象简介


顾名思义，互斥体对象是设计用于确保在一组内核模式线程间共享的单个资源相互独占访问的同步机制。 仅最高级别的驱动程序，例如文件系统驱动程序 (FSDs) 使用 executive 工作线程，很可能使用互斥体对象。

可能是最高级别的驱动程序和驱动程序创建的线程或工作线程回调例程可能会使用互斥体对象。 但是，任何驱动程序和使用可分页的线程或工作线程回调例程必须管理收购的等待和它的互斥体对象的版本应非常小心。

互斥体对象具有内置功能可提供系统 （仅内核模式） 线程互相排斥，死锁释放 SMP 计算机中的共享资源的访问。 内核一次将 mutex 的所有权分配给单个线程。

获取 mutex 的所有权阻止交付的正常的内核模式下异步过程调用 (Apc)。 该线程将不会被占用 APC 除非内核发出 APC\_级软件中断运行一个特殊内核 APC，如结果返回到原始请求方的 I/O 操作的 I/O 管理器的 IRP 完成例程

一个线程可以获取互斥体对象，它已拥有 （递归所有权），但以递归方式获取互斥体对象未设置为用信号通知状态，直到线程完全释放其所有权的所有权。 此类线程必须显式释放该互斥体无数次，它之前另一个线程可以获取互斥体获取所有权。

内核永远不会允许拥有互斥体，而无需第一个释放互斥体，然后将其设置为用信号通知状态导致转换为用户模式的线程。 如果拥有互斥体的任何 FSD 创建或驱动程序创建线程尝试在释放 mutex 的所有权之前将控制返回给 I/O 管理器，内核会停止系统。

任何驱动程序，它使用互斥体对象必须调用[ **KeInitializeMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff552147)等待或释放其互斥体对象之前的一次。 下图说明了两个系统线程可能会使用互斥体对象。

![说明等待 mutex 对象的关系图](images/3mutxobj.png)

上图所示，使用互斥体对象的驱动程序必须为 mutex 对象，它必须是常驻提供存储。 可以使用该驱动程序[设备扩展](device-extensions.md)的驱动程序创建的设备对象，如果它使用的控制器扩展[控制器对象](using-controller-objects.md)，或由驱动程序分配的非分页缓冲的池。

当驱动程序调用**KeInitializeMutex** (通常是从其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程)，它必须将一个指针传递给该互斥体对象的驱动程序的存储的内核初始化到用信号通知状态。

这样的最高级别的驱动程序已初始化后，它可以管理相互独占访问共享资源，如在上图中所示。 例如，驱动程序的本质上的同步操作和线程的调度例程可能会使用互斥体的 Irp 保护驱动程序创建队列。

因为**KeInitializeMutex**始终 mutex 对象的初始状态设置为用信号通知 （如前面图所示）：

1.  调度例程的首次调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)与*互斥体*指针使当前线程立即进入就绪状态，提供线程互斥体的所有权和互斥体状态重置为未发出信号。 尽快调度例程继续运行，它可以安全地将 IRP 插入 mutex 保护队列。

2.  当第二个线程 （另一个调度例程，驱动程序所提供的工作线程回调例程或驱动程序创建的线程） 调用**KeWaitForSingleObject**与*互斥体*指针，第二个线程将处于等待状态。

3.  当调度例程完成队列中所述的步骤 1 作为 IRP 时，它将调用[ **KeReleaseMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553140)与*互斥体*指针和一个布尔值*等待*值，该值指示是否打算调用**KeWaitForSingleObject** (或[ **KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)) 与*Mutex*只要**KeReleaseMutex**返回控件。

4.  假设的调度例程释放其所有权的步骤 3 中互斥体 (*等待*设置为**FALSE**)，该互斥体设置为通过用信号通知状态**KeReleaseMutex**。 互斥体当前有没有所有者，因此内核确定是否另一个线程正在等待该互斥体。 如果内核，使第二个线程 （请参阅步骤 2） 的互斥体所有者可能提升到实时优先级值最低的线程的优先级以及更改其状态为就绪。

5.  内核为处理器可调度第二个线程中的执行： 即，当具有较高优先级没有其他线程当前处于就绪状态和有要在更高版本的 IRQL 运行没有内核模式例程。 第二个线程 （队列 IRP 的调度例程或驱动程序的工作线程回调例程或出队 IRP 的驱动程序创建的线程） 现在可以安全地访问受保护的互斥体的 Irp 队列之前它将调用**KeReleaseMutex**。

如果一个线程获取互斥体对象以递归方式的所有权，必须显式调用该线程**KeReleaseMutex**无数次，互斥体等待以互斥体对象设置为用信号通知状态。 例如，如果某个线程调用**KeWaitForSingleObject** ，然后**KeWaitForMutexObject**具有相同*互斥体*指针，它必须调用**KeReleaseMutex**两次时它将获取互斥体以将该互斥体对象设置为用信号通知状态。

调用**KeReleaseMutex**与*等待*参数设置为**TRUE**指示调用方的意图立即调用**KeWait * Xxx*** 支持在从返回的例程**KeReleaseMutex**。

**请考虑将等待参数设置为 KeReleaseMutex 时遵循以下原则：**

可分页的线程或在被动 IRQL 运行的可分页的驱动程序例程\_级别应永远不会调用**KeReleaseMutex**与*等待*参数设置为**TRUE**. 此类调用会导致严重的页面错误，如果调用方碰巧换出到调用之间**KeReleaseMutex**并**KeWait*Xxx*对象**(s)。

在晚于被动的 IRQL 运行任何标准驱动程序例程\_级别不能等待非零值的时间间隔上的所有调度程序对象而不会降低关闭系统。 但是，可以调用此类例程**KeReleaseMutex**如果拥有该互斥体的 IRQL 小于或等于在调度到的运行时\_级别。

在运行的标准驱动程序例程于 Irql 的摘要，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

 

 




