---
title: 定义和使用事件对象
description: 定义和使用事件对象
ms.assetid: 4b7807f0-bbea-4402-b028-9ac73724717f
keywords:
- 事件对象 WDK 内核
- 正在等待对事件对象
- 同步事件 WDK 内核
- 通知事件 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40431afc5dd1a2b8117c519cfbb916338c20bf46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388252"
---
# <a name="defining-and-using-an-event-object"></a>定义和使用事件对象





使用一个事件对象的任何驱动程序必须调用[ **KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)， [ **IoCreateNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549039)，或[**IoCreateSynchronizationEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff549045)等待之前，请设置、 清除，或重置该事件。 下图说明了如何与线程的驱动程序可以使用一个事件对象进行同步。

![说明等待一个事件对象的关系图](images/3evntobj.png)

上图所示，这样的驱动程序必须为事件对象，它必须是常驻提供存储。 可以使用该驱动程序[设备扩展](device-extensions.md)的驱动程序创建的设备对象，如果它使用的控制器扩展[控制器对象](using-controller-objects.md)，或由驱动程序分配的非分页缓冲的池。

当驱动程序调用**KeInitializeEvent**，它必须将一个指针传递给驱动程序的常驻存储事件对象。 此外，调用方必须指定初始状态 （发出信号或不处于终止状态） 的事件对象。 调用方还必须指定事件类型，它可以是以下值：

-   **SynchronizationEvent**

    当*同步事件*设置到用信号通知的状态，等待被重置为未用信号通知的事件的单线程变得符合条件执行和事件的状态自动重置为未用信号通知。

    此类型的事件有时称为*未事件*，因为它用信号通知的状态在等待满足每次自动重置。

-   **NotificationEvent**

    当*通知事件*设置为用信号通知状态，在等待着要重置为未用信号通知的事件的所有线程有资格成为执行和事件到显式重置前保持用信号通知状态不发出信号发生： 即，没有调用[ **KeClearEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff551980)或[ **KeResetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553176)与给定*事件*指针。

几个设备或中间驱动程序有一个驱动程序专用线程，让我们单独一组可能会等待进行保护的共享的资源的事件同步其操作的线程。

使用事件对象以等待 I/O 操作的完成设置输入的大多数驱动程序*类型*到**notificationevent 将**当它们调用**KeInitializeEvent**。 事件对象设置为一个驱动程序将创建具有的 Irp [ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)或[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)几乎总是初始化为**notificationevent 将**因为调用方将等待一个或多个较低级别驱动程序，满足其请求的通知的事件。

后驱动程序已初始化自身，其驱动程序专用的线程，如果有，和其他例程可以同步其事件的操作。 例如，与管理系统软盘控制器驱动程序，如队列 Irp，线程的驱动程序可能同步 IRP 处理事件，如在上图中所示：

1.  线程已取消排队的设备上处理 IRP，调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)用一个指针指向已初始化的事件对象的驱动程序提供存储。

2.  其他驱动程序例程执行设备满足 IRP，和这些操作都完成后，驱动程序的所需的 I/O 操作数[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程调用[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)用一个指针指向事件对象，驱动程序确定优先级提升线程 (*增量*，如在上图中所示)，和一个布尔值*等待*设置为**FALSE**。 调用**KeSetEvent**将事件对象设置为用信号通知状态，从而更改正在等待线程的状态变为就绪。

3.  内核为处理器可调度线程中的执行： 即，具有较高优先级没有其他线程当前处于就绪状态和有要在更高版本的 IRQL 运行没有内核模式例程。

    该线程现在可以完成 IRP 如果*DpcForIsr*但调用**IoCompleteRequest**与 IRP，和可以取消排队的另一个 IRP，若要在设备上进行处理。

调用**KeSetEvent**与*等待*参数设置为**TRUE**指示调用方的意图立即调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)或[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)支持例程返回时从**KeSetEvent**。

**请考虑下面的设置的指导***等待***参数 toKeSetEvent:**

可分页的线程或在 IRQL 运行的可分页的驱动程序例程&lt;调度\_级别应永远不会调用**KeSetEvent**与*等待*参数设置为 **，则返回 TRUE**. 此类调用会导致严重的页面错误，如果调用方碰巧换出到调用之间**KeSetEvent**并**KeWaitForSingleObject**或**KeWaitForMultipleObjects**。

在 IRQL 运行任何标准驱动程序例程 = 调度\_级别不能等待非零值的时间间隔上的所有调度程序对象而不会降低关闭系统。 但是，可以调用此类例程**KeSetEvent**调度的 IRQL 小于或等于在运行时\_级别。

在运行的标准驱动程序例程于 Irql 的摘要，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

**KeResetEvent**返回的前一状态给定*事件*： 是否它已设置为用信号通知或不时对调用**KeResetEvent**发生。 **KeClearEvent**只需设置的状态的给定*事件*为非终止。

**请考虑以下有关何时调用上述支持例程指南：**

为了提高性能，每个驱动程序应调用**KeClearEvent**除非调用方需要返回的信息**KeResetEvent**来确定要执行的下一步操作。

 

 




