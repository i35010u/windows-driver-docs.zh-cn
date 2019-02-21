---
title: 编写 DPC 例程准则
description: 编写 DPC 例程准则
ms.assetid: 570219be-d152-4826-855a-737bbed67ffd
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc6b179d708942de114158b1430763815a8ef22c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543496"
---
# <a name="guidelines-for-writing-dpc-routines"></a>编写 DPC 例程准则





编写时记住以下几点[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程：

-   一个*DpcForIsr*或*CustomDpc*例程必须同步到物理设备时，其访问权限和对共享的状态的任何信息或资源维护驱动程序，但使用驱动程序的其他例程的访问相同的设备或内存位置。

    如果*DpcForIsr*或*CustomDpc*例程与 ISR 共享设备或状态时，必须调用[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)提供驱动程序提供的地址[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程的程序在设备或访问共享的状态。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

    如果*DpcForIsr*或*CustomDpc*例程共享状态或资源，例如联锁的队列或具有 ISR 以外的例程的计时器对象，它必须保护共享的状态或使用的资源驱动程序初始化 executive 自旋锁。 有关详细信息，请参阅[旋转锁](spin-locks.md)。

-   *DpcForIsr*并*CustomDpc*例程运行在 IRQL = 调度\_级别，限制可以调用的支持例程集。

    例如， *DpcForIsr*并*CustomDpc*例程不能访问或分配可分页内存，并且不能等待[内核调度程序对象](kernel-dispatcher-objects.md)设置为发出信号状态。 但是，它们可以获取和释放使用的驱动程序的执行数值调节钮锁[ **KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)并[ **KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150)，它运行速度更快比**KeAcquireSpinLock**并**KeReleaseSpinLock**。

    尽管 DPC 例程不能进行阻塞调用，但可以在中运行的工作项进行排队[系统工作线程](system-worker-threads.md)运行在 IRQL = 被动\_级别。 工作项可以等待调度程序对象的阻止调用。 若要将工作项，排队*DpcForIsr*例程通常如调用例程[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)，和一个*CustomDpc*例程通常会调用[ **ExQueueWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff540216)例程。

-   *DpcForIsr*并*CustomDpc*例程是通常负责启动下一步的 I/O 操作在设备上。

    使用直接 I/O 的最低级别的物理设备驱动程序，此职责可能包括将[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程进行编程设备将传输更多的数据才能符合要求驱动程序调用之前的当前 IRP [ **IoStartNextPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550358)。

-   *DpcForIsr*并*CustomDpc*例程的短暂期间内，只应运行，并且应委托以尽可能接近工作线程太多处理。

    上一个处理器的 DPC 例程时，会阻止所有线程在同一个处理器上运行。 排队并准备好运行的其他 DPC 例程可以阻止执行，直到完成当前的 DPC 例程。 若要避免降低系统的响应能力，典型的 DPC 例程应运行不超过 100 个微秒次调用时。 如果任务需要超过 100 微秒为单位，并且必须执行在 IRQL = 调度\_级别，DPC 例程后，应该结束 100 微秒以下且一个或多个计划[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)若要在以后完成任务的例程。 有关详细信息*CustomTimerDpc*例程，请参阅[计时器对象和 dpc 进行标记](timer-objects-and-dpcs.md)。

    DPC 例程应仅执行的任务，都必须运行在调度\_级别，然后委托所有剩余中断相关的工作线程运行的 IRQL = 被动\_级别。 例如，一个 DPC 例程可以排入队列要在中运行的工作项[系统工作线程](system-worker-threads.md)。

    DPC 调用的例程[ **KeStallExecutionProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff553295)来延迟执行的例程不能指定多个 100 微秒为单位的延迟。

    使用在 WDK 中的性能分析工具来评估 DPC 例程的执行时间。 有关使用示例[Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994)工具来监视 DPC 执行时间，请参阅[示例 15:测量 DPC/ISR 时间](https://msdn.microsoft.com/library/windows/hardware/ff545764)。

-   如果驱动程序使用 DMA 并将其[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程返回**KeepObject**或者**DeallocateObjectKeepRegisters** （从而保留系统 DMA 控制器通道或其他传输操作的主机总线适配器）， *DpcForIsr*或*CustomDpc*例程会释放适配器对象或映射中注册[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)或[ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)完成当前之前IRP，并返回控件。

-   如果最低级别的物理设备驱动程序设置了[控制器对象](using-controller-objects.md)同步 I/O 操作通过控制器到连接的设备，其*DpcForIsr*或*CustomDpc*例程会释放控制器对象使用[ **IoFreeController** ](https://msdn.microsoft.com/library/windows/hardware/ff549104)完成当前的 IRP，并将控件返回之前。

-   *DpcForIsr*并*CustomDpc*例程是通常负责给定请求，如果有必要，并且有可能，以及重试当前请求的处理过程中出现的任何设备错误日志记录设置 I/O 状态块以及调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)当前 IRP 的。

-   如果驱动程序和设备支持重叠的 I/O 操作，该驱动程序必须遵循的规则[处理重叠的 I/O 操作](handling-overlapped-i-o-operations.md)。

-   *DpcForIsr*或*CustomDpc*的任何驱动程序例程通常完成 I/O 处理，仅为子集公共的 I/O 控制代码的驱动程序必须支持。 具体而言，DPC 例程完成操作的设备控制请求具有以下特征：
    -   将物理设备的状态更改的请求
    -   要求返回有关物理设备本身不稳定信息请求

 

 




