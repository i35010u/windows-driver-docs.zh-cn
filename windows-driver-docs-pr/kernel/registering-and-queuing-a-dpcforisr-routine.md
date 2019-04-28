---
title: DpcForIsr 例程注册和排队
description: DpcForIsr 例程注册和排队
ms.assetid: 32253573-842e-40bc-9616-8d1ccd7afa29
keywords:
- DpcForIsr
- 注册 DpcForIsr 例程
- 队列 DpcForIsr 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b8188826a55749d87c4f3a679088ec89a12d19a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352987"
---
# <a name="registering-and-queuing-a-dpcforisr-routine"></a>DpcForIsr 例程注册和排队





驱动程序注册[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程对于设备对象通过调用[ **IoInitializeDpcRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549307)它在创建后设备对象。 该驱动程序可以进行此调用从其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，或从[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)处理代码[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。

到队列*DpcForIsr*执行例行，驱动程序的 ISR 调用[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)之前它将返回。 下图说明了对这些例程的调用。

![关系图说明如何使用 dpc 对象进行 dpcforisr 例程](images/3dpcisr.png)

上图所示，调用**IoInitializeDpcRequest** DPC 对象相关联的驱动程序提供*DpcForIsr*例程和驱动程序创建的设备对象。 I/O 管理器分配内存的 DPC 对象并调用[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)驱动程序的代表。

当 ISR 调用以处理在 DIRQL 的设备中断时，它应返回控件到系统尽可能快地进行更好的整体系统和驱动程序性能。 通常情况下，ISR 只是清除中断，会收集任何上下文的信息*DpcForIsr*例程需要完成此操作导致的中断，调用[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)，并返回。

当调用 ISR **IoRequestDpc**，它将指针传递到的设备对象，指向*DeviceObject*-&gt;**CurrentIrp**，和一个到驱动程序确定上下文的指针。 I/O 管理器调用[ **KeInsertQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552185)驱动程序的代表的队列 DPC 对象。 当 IRQL 低于调度\_级别上是处理器，内核取消排队 DPC 对象和运行驱动程序的*DpcForIsr*例程在 IRQL 调度该处理器上\_级别。

*DpcForIsr*例程负责执行会尽一切努力完成当前的 IRP 中请求的 I/O。 在进入时，该例程接收指向 DPC 对象，以及对 ISR 的调用中传递到设备对象、 IRP 和上下文区域的指针的指针**IoRequestDpc**。 上下文区域必须在常驻内存中，并且通常是在设备扩展。 或者，它可以是分配驱动程序，或在控制器扩展中，如果驱动程序使用的非分页缓冲池[控制器对象](using-controller-objects.md)。

因为 ISR 和*DpcForIsr*例程可以 SMP 计算机上同时运行，必须遵守以下原则：

-   必须调用 ISR **IoRequestDpc**之前它将返回控制。 否则为*DpcForIsr* ISR 完成的上下文区域设置之前，可能会在另一个处理器上运行例程*DpcForIsr*例程。

-   *DpcForIsr*例程，并与 ISR 共享上下文区域的任何其他驱动程序例程必须调用[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)，指定驱动程序提供[*SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)以包含多个处理器安全的方式访问的共享的上下文区域的例程。

-   如果驱动程序使用设备扩展来维护有关其设备 I/O 操作，上下文*DpcForIsr*应永远不会调用例程[ **IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)输入设备对象 （或如果该驱动程序管理其自己 IRP 队列取消排队的输入的设备对象 IRP） 之前只是调用之前[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    否则为驱动程序的[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858) （或队列管理例程） 可能会开始将覆盖之前的共享的上下文区域的另一 I/O 操作*DpcForIsr*例程可以完成当前操作。 这是因为如果设备中断时或之前可以再次调用 ISR *DpcForIsr*例程执行 （假定中断仍处于启用状态）。

在单处理器计算机上甚至 ISR 无法再次调用如果时或之前，设备中断*DpcForIsr*运行例程。 如果发生这种情况， *DpcForIsr*例程仅运行一次。 换而言之，没有一对一的对应关系 ISR 调用之间**IoRequestDpc**和的实例化*DpcForIsr*如果驱动程序与重叠其目标设备的 I/O 操作的例程对象。

 

 




