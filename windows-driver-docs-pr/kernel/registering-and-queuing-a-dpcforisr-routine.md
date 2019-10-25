---
title: DpcForIsr 例程注册和排队
description: DpcForIsr 例程注册和排队
ms.assetid: 32253573-842e-40bc-9616-8d1ccd7afa29
keywords:
- DpcForIsr
- 注册 DpcForIsr 例程
- 排队 DpcForIsr 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4db9544d8015cec00c5860b83b1f19690e89907a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827504"
---
# <a name="registering-and-queuing-a-dpcforisr-routine"></a>DpcForIsr 例程注册和排队





驱动程序在创建设备对象之后，通过调用[**IoInitializeDpcRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializedpcrequest)为设备对象注册[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程。 驱动程序可以从其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程或从处理[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求的[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)代码进行此调用。

若要将*DpcForIsr*例程排队以便执行，驱动程序的 ISR 会在返回之前调用[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc) 。 下图说明了对这些例程的调用。

![说明如何将 dpc 对象用于 dpcforisr 例程的关系图](images/3dpcisr.png)

如上图所示，调用**IoInitializeDpcRequest**将 DPC 对象与驱动程序提供的*DpcForIsr*例程和驱动程序创建的设备对象相关联。 I/o 管理器为 DPC 对象分配内存并代表驱动程序调用[**KeInitializeDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc) 。

当调用 ISR 来处理 DIRQL 处的设备中断时，它应尽快将控制权返还给系统，以获得更好的整体系统和驱动程序性能。 通常情况下，ISR 仅清除中断，收集*DpcForIsr*例程完成导致中断的操作所需的任何上下文信息，调用[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)，并返回。

当 ISR 调用**IoRequestDpc**时，它将传递指向设备对象的指针、指向*DeviceObject*-的指针&gt;**CurrentIrp**，以及指向驱动程序确定的上下文的指针。 I/o 管理器代表驱动程序调用[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc) ，这会将 DPC 对象排队。 如果在处理器上的 IRQL 低于调度\_级别，则内核取消排队 DPC 对象，并以 IRQL 调度\_级别在该处理器上运行驱动程序的*DpcForIsr*例程。

*DpcForIsr*例程负责执行完成当前 IRP 中请求的 i/o 所需的一切。 进入时，例程会接收指向 DPC 对象的指针，以及指向设备对象、IRP 和上下文区域的指针，这些指针在 ISR 对**IoRequestDpc**的调用中传递。 上下文区域必须在常驻内存中，并且通常位于设备扩展中。 或者，它可以位于由驱动程序分配的非分页池中，如果驱动程序使用[控制器对象](using-controller-objects.md)，则也可以位于控制器扩展中。

由于 ISR 和*DpcForIsr*例程可以在 SMP 计算机上并发运行，因此必须遵循以下准则：

-   ISR 在返回 control 之前，必须先调用**IoRequestDpc** 。 否则，在 ISR 完成*DpcForIsr*例程的上下文区域设置之前， *DpcForIsr*例程可能在另一个处理器上运行。

-   与 ISR 共享上下文区域的*DpcForIsr*例程和其他任何驱动程序例程都必须调用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)，并指定驱动程序提供的用于访问中的共享上下文区域的[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程多处理器安全的方式。

-   如果驱动程序使用设备扩展来维护有关其设备 i/o 操作的上下文，则*DpcForIsr*例程绝不应为输入设备对象调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) （如果驱动程序管理自己的 IRP 队列），直到调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    否则，驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) （或队列管理例程）可能会开始另一个 i/o 操作，该操作将覆盖共享上下文区域，然后*DpcForIsr*例程才能完成当前操作。 这是因为，如果设备在*DpcForIsr*例程执行期间或之前中断，则可以再次调用 ISR （假设仍启用了中断）。

即使在单处理器计算机上，如果在运行*DpcForIsr*例程时或之前中断设备，也可以再次调用 ISR。 如果发生这种情况， *DpcForIsr*例程只运行一次。 换句话说，如果驱动程序的目标设备对象的 i/o 操作重叠，则 ISR 对**IoRequestDpc**的调用和*DpcForIsr*例程的实例化之间不存在一对一的对应关系。

 

 




