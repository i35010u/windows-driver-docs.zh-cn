---
title: 互斥对象简介
description: 互斥对象简介
ms.assetid: c35b4341-09dd-411d-b933-6c762fecd23c
keywords:
- 内核调度程序对象 WDK，mutex 对象
- 调度程序对象 WDK 内核，mutex 对象
- mutex 对象 WDK 内核
- 互斥访问 WDK 内核
- 正在等待 mutex 对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5398f34435f95d797d9d6ef82e76731a52dd8725
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828188"
---
# <a name="introduction-to-mutex-objects"></a>互斥对象简介


顾名思义，mutex 对象是一种同步机制，旨在确保对在一组内核模式线程之间共享的单个资源进行相互独立的访问。 只有最上层的驱动程序（如使用执行器工作线程的文件系统驱动程序（FSDs））才可能使用 mutex 对象。

使用驱动程序创建的线程或工作线程回调例程的最高级别的驱动程序可能使用互斥体对象。 但是，具有可分页线程或工作线程回调例程的任何驱动程序都必须仔细管理其 mutex 对象的购置、等待和释放。

Mutex 对象具有内置功能，这些功能提供了系统（仅限内核模式）线程互相排斥，无需在 SMP 计算机中访问共享资源。 内核一次将 mutex 的所有权分配给单个线程。

获取互斥体的所有权会阻止正常内核模式异步过程调用（Apc）的传递。 除非内核发出 APC\_级别软件中断来运行特殊内核 APC （如 i/o 管理器的 IRP 完成例程，该例程会将结果返回给 i/o 操作的原始请求方），否则线程将不被 APC 抢占

线程可以获取它已拥有的 mutex 对象的所有权（递归所有权），但递归获取的 mutex 对象不会设置为终止状态，直到线程完全释放其所有权。 此类线程必须明确地释放 mutex，因为它获取所有权，而另一个线程可以获取互斥体。

内核从不允许拥有互斥体的线程导致转换到用户模式，而无需先释放互斥体，然后将其设置为终止状态。 如果任何 FSD 创建的或驱动程序创建的线程在释放互斥体的所有权之前尝试将控制权返回给 i/o 管理器，内核会关闭系统。

使用 mutex 对象的任何驱动程序在等待或释放其 mutex 对象之前，都必须调用[**KeInitializeMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializemutex)一次。 下图说明两个系统线程可能使用 mutex 对象的方式。

![说明如何等待 mutex 对象的关系图](images/3mutxobj.png)

如上图所示，使用 mutex 对象的驱动程序必须为必须驻留的 mutex 对象提供存储。 驱动程序可以使用驱动程序创建的设备对象的[设备扩展](device-extensions.md)，如果控制器扩展使用[控制器对象](using-controller-objects.md)或由驱动程序分配的非分页池，则可以使用控制器扩展。

当驱动程序调用**KeInitializeMutex** （通常来自其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程）时，它必须为 mutex 对象传递一个指向该驱动程序存储区的指针，该对象内核初始化为终止状态。

此类高级驱动程序初始化完成后，可以按上图所示管理对共享资源的相互独占的访问。 例如，对于原本同步操作和线程，驱动程序的调度例程可能使用互斥体来保护用于 Irp 的驱动程序创建的队列。

因为**KeInitializeMutex**始终将互斥体对象的初始状态设置为 "已终止" （如上图所示）：

1.  调度例程使用*mutex*指针对[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)进行的初始调用会将当前线程立即置于就绪状态，赋予互斥体的线程所有权，并将互斥体状态重置为未发出信号。 一旦派单例程恢复运行，它就可以安全地将 IRP 插入受互斥体保护的队列中。

2.  当第二个线程（另一个调度例程、驱动程序*提供的工作*线程回调例程或驱动程序创建的线程）调用**KeWaitForSingleObject**时，会将第二个线程置于等待状态。

3.  当调度例程按照步骤1中的说明完成对 IRP 的排队时，它将使用*Mutex*指针调用[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) ，并使用布尔*等待*值来指示它是否打算调用**KeWaitForSingleObject** （或[**KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)）， **KeReleaseMutex**返回 control 后，就会出现*互斥体*。

4.  假设调度例程在步骤3（*等待*设置为**FALSE**）中释放了互斥体的所有权，则会通过**KeReleaseMutex**将互斥体设置为终止状态。 Mutex 当前没有所有者，因此内核确定另一个线程是否正在等待该互斥体。 如果是这样，内核将使第二个线程（请参阅步骤2）成为 mutex 所有者，可能将线程的优先级提升到最低的实时优先级值，并将其状态更改为 "就绪"。

5.  当处理器可用时，内核会立即调度第二个线程执行：也就是说，如果没有具有较高优先级的其他线程当前处于就绪状态，并且没有要在更高的 IRQL 上运行的内核模式例程，则为。 在调用**KeReleaseMutex**之前，第二个线程（将 irp 或驱动程序的工作线程回调例程或驱动程序创建的线程出列）的第二个线程可以安全地访问 irp 的受 mutex 保护的队列。

如果线程以递归方式获取互斥体对象的所有权，则该线程必须多次显式调用**KeReleaseMutex** ，因为它会在互斥体上等待，以将 mutex 对象设置为终止状态。 例如，如果一个线程调用**KeWaitForSingleObject** ，然后使用相同的*Mutex*指针调用**KeWaitForMutexObject** ，则它在获取互斥体时必须调用**KeReleaseMutex**两次，以便将该 mutex 对象设置为发出信号状态.

如果调用**KeReleaseMutex** ，并将*Wait*参数设置为**TRUE** ，则指示调用方在从**KeReleaseMutex**返回时立即调用**KeWait * Xxx*** 支持例程。

**请考虑以下将 Wait 参数设置为 KeReleaseMutex 的准则：**

以 IRQL 被动\_级别运行的可分页线程或可分页的驱动程序例程不应调用**KeReleaseMutex** ，并将*Wait*参数设置为**TRUE**。 如果调用方在对**KeReleaseMutex**和**KeWait*Xxx*对象**的调用之间分页，则此类调用将导致严重的页错误。

任何以 IRQL 大于被动\_级别运行的标准驱动程序例程都不会在不关闭系统的情况下等待任何调度程序对象上的非零间隔。 但是，如果在其上运行的 mutex 小于或等于调度\_级别，则此类例程可以调用**KeReleaseMutex** 。

有关标准驱动程序例程运行的 IRQLs 的摘要，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

 

 




