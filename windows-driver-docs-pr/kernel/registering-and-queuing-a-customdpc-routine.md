---
title: CustomDpc 例程注册和排队
description: CustomDpc 例程注册和排队
keywords:
- CustomDpc
- 注册 CustomDpc 例程
- 排队 CustomDpc 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16b37cda30586a0f16fc58475e65a67d0a383e03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837987"
---
# <a name="registering-and-queuing-a-customdpc-routine"></a>CustomDpc 例程注册和排队





驱动程序在创建设备对象之后，通过调用 [**KeInitializeDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)为设备对象注册 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程。 驱动程序可以从其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程或处理 [**IRP \_ MN \_ 开始 \_ 设备**](./irp-mn-start-device.md)请求的 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)代码进行此调用。

紧靠驱动程序的 ISR 返回 control 之前，它可以调用 [**KeInsertQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc) 将 *CustomDpc* 例程排队等待执行。 下图说明了对这些例程的调用。

![说明如何将 dpc 对象用于 customdpc 例程的关系图](images/3cstmdpc.png)

如上图所示，具有 *CustomDpc* 例程的驱动程序必须提供 DPC 对象的存储。 由于驱动程序必须通过其 ISR 传递指向 DPC 对象的指针，因此存储必须位于驻留的系统空间内存中。 大多数包含 *CustomDpc* 例程的驱动程序在设备扩展中为其 DPC 对象提供存储，但如果驱动程序使用 [控制器对象](./introduction-to-controller-objects.md) 或由驱动程序分配的非分页池，则存储可以位于控制器扩展中。

当驱动程序调用 **KeInitializeDpc** 时，它必须传递其 *CustomDpc* 例程的入口点，以及指向 DPC 对象的驱动程序分配的存储和驱动程序定义的上下文区域的指针（在调用时传递到 *CustomDpc* 例程）。 由于上下文区域必须可在 IRQL = 调度级别进行访问 \_ ，因此它还必须位于驻留内存中。

与 *DpcForIsr* 例程不同， *CustomDpc* 例程不与设备对象相关联。 尽管如此，驱动程序通常还包括指向目标设备对象和当前 IRP 的指针（提供给 *CustomDpc* 例程的上下文信息）。 与 *DpcForIsr* 例程一样， *CustomDpc* 例程使用此信息来完成中断驱动的 I/O 操作，其 IRQL 低于 ISR。

如上图所示，ISR 向 DPC 对象传递指向 DPC 对象的指针，并向 [**KeInsertQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)传递另外两个由驱动程序定义的参数。 如果计算机中的所有处理器当前的代码在 IRQL 大于或等于调度级别的情况下运行 \_ ，则 DPC 对象将排队等待，直到 irql 低于 \_ 处理器上的调度级别。 然后，核心取消排队 DPC 对象，驱动程序的 *CustomDpc* 例程在处理器上以 IRQL 调度 \_ 级别运行。

在任意给定时刻，只能对任何一个 DPC 对象的单个实例化进行排队。 因此，如果 ISR 在运行驱动程序的 *CustomDpc* 例程之前使用同一个 *Dpc* 指针多次调用 **KeInsertQueueDpc** ，则 *CustomDpc* 例程仅在 IRQL 低于处理器上的调度级别后运行一次 \_ 。

*CustomDpc* 例程负责执行完成导致中断的 i/o 操作所需的任何操作。

ISR 和 *CustomDpc* 例程可以在 SMP 计算机上并发运行。 因此，在编写 *CustomDpc* 例程时，请遵循上一部分中所述的指导原则， [注册和排队 DpcForIsr 例程](registering-and-queuing-a-dpcforisr-routine.md)。

 

