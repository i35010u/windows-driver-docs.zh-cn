---
title: CustomDpc 例程注册和排队
description: CustomDpc 例程注册和排队
ms.assetid: 7c35f8f8-a6dc-43b1-9120-701227d7b4c5
keywords:
- CustomDpc
- 注册 CustomDpc 例程
- 排队 CustomDpc 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aeacfc3b2ae1c8fddcb53e7f31fa55ac56e87ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827513"
---
# <a name="registering-and-queuing-a-customdpc-routine"></a>CustomDpc 例程注册和排队





驱动程序在创建设备对象之后，通过调用[**KeInitializeDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)为设备对象注册[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程。 驱动程序可以从其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程或从处理[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求的[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)代码进行此调用。

紧靠驱动程序的 ISR 返回 control 之前，它可以调用[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)将*CustomDpc*例程排队等待执行。 下图说明了对这些例程的调用。

![说明如何将 dpc 对象用于 customdpc 例程的关系图](images/3cstmdpc.png)

如上图所示，具有*CustomDpc*例程的驱动程序必须提供 DPC 对象的存储。 由于驱动程序必须通过其 ISR 传递指向 DPC 对象的指针，因此存储必须位于驻留的系统空间内存中。 大多数包含*CustomDpc*例程的驱动程序在设备扩展中为其 DPC 对象提供存储，但如果驱动程序使用[控制器对象](using-controller-objects.md)或由驱动程序分配的非分页池，则存储可以位于控制器扩展中。

当驱动程序调用**KeInitializeDpc**时，它必须传递其*CustomDpc*例程的入口点，以及指向 DPC 对象的驱动程序分配的存储以及驱动程序定义的上下文区域（传递到*CustomDpc*调用例程。 由于上下文区域必须可在 IRQL = 调度\_级别访问，因此它还必须位于驻留内存中。

与*DpcForIsr*例程不同， *CustomDpc*例程不与设备对象相关联。 尽管如此，驱动程序通常还包括指向目标设备对象和当前 IRP 的指针（提供给*CustomDpc*例程的上下文信息）。 与*DpcForIsr*例程一样， *CustomDpc*例程使用此信息来完成中断驱动的 I/O 操作，其 IRQL 低于 ISR。

如上图所示，ISR 向 DPC 对象传递指向 DPC 对象的指针，并向[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)传递另外两个由驱动程序定义的参数。 如果计算机中的所有处理器当前的代码以大于或等于调度\_级别的 IRQL 运行，则 DPC 对象将排队等候，直到 IRQL 降到低于\_对处理器的级别。 然后，核心取消排队 DPC 对象和驱动程序的*CustomDpc*例程在上的 IRQL 调度\_级别运行。

在任意给定时刻，只能对任何一个 DPC 对象的单个实例化进行排队。 因此，如果 ISR 在运行驱动程序的*CustomDpc*例程之前使用同一个*Dpc*指针多次调用**KeInsertQueueDpc** ，则*CustomDpc*例程仅在以下情况下运行一次：在对处理器\_级别进行调度之后。

*CustomDpc*例程负责执行完成导致中断的 i/o 操作所需的任何操作。

ISR 和*CustomDpc*例程可以在 SMP 计算机上并发运行。 因此，在编写*CustomDpc*例程时，请遵循上一部分中所述的指导原则，[注册和排队 DpcForIsr 例程](registering-and-queuing-a-dpcforisr-routine.md)。

 

 




