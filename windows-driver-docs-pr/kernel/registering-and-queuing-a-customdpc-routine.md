---
title: CustomDpc 例程注册和排队
description: CustomDpc 例程注册和排队
ms.assetid: 7c35f8f8-a6dc-43b1-9120-701227d7b4c5
keywords:
- CustomDpc
- 注册 CustomDpc 例程
- 队列 CustomDpc 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8f265a45fd052996cc52fbe068b8e1b2490306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391102"
---
# <a name="registering-and-queuing-a-customdpc-routine"></a>CustomDpc 例程注册和排队





驱动程序注册[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程对于设备对象通过调用[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)创建设备后对象。 该驱动程序可以进行此调用从其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，或从[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)处理代码[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。

驱动程序的 ISR 只返回控件之前，它可以调用[ **KeInsertQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552185)到队列*CustomDpc*例程的执行。 下图说明了对这些例程的调用。

![关系图说明如何使用 dpc 对象进行 customdpc 例程](images/3cstmdpc.png)

上图所示，驱动程序，包含*CustomDpc*例程必须为 DPC 对象提供存储。 因为该驱动程序必须从其 ISR 将指针传递给 DPC 对象，存储必须位于常驻，系统空间内存中。 与大多数驱动程序*CustomDpc*例程提供存储在设备扩展中，其 DPC 对象，但如果驱动程序使用，存储可在控制器扩展[控制器对象](using-controller-objects.md)或在非分页该驱动程序分配的池。

当驱动程序调用**KeInitializeDpc**，它必须传递给入口点及其*CustomDpc*例程，以及到 DPC 对象的驱动程序分配存储和驱动程序定义的上下文的指针区域中，传递给*CustomDpc*例程时调用它。 因为上下文区域必须是可访问在 IRQL = 调度\_级别，它还必须在常驻内存中。

与不同*DpcForIsr*例程*CustomDpc*例程不是与设备对象相关联。 然而，驱动程序通常包括指向目标设备对象的指针，并且当前 IRP 中的上下文信息提供给*CustomDpc*例程。 像*DpcForIsr*例程*CustomDpc*例程使用此信息来完成比 ISR 降低 IRQL 在中断驱动 I/O 操作

上图所示，ISR 将指针传递到 DPC 对象和两个其他参数，这些驱动程序定义的为参数[ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)。 如果在计算机中的所有处理器当前都有代码运行在 IRQL 大于或等于调度\_级别、 DPC 对象会排队，直到 IRQL 低于调度\_级别处理器上。 然后，内核 DPC 对象，并在驱动程序中取消排队*CustomDpc* IRQL 调度在处理器上运行时例程\_级别。

可以在任意给定时刻排队仅 DPC 的任何一个对象的单一实例化。 因此如果 ISR 调用**KeInsertQueueDpc**多个具有相同的一次*Dpc*之前驱动程序的指针*CustomDpc*运行时例程， *CustomDpc*例程只运行一次后 IRQL 低于调度\_级别处理器上。

一个*CustomDpc*例程负责执行会尽一切努力完成 I/O 操作导致中断。

ISR 和*CustomDpc*例程可以 SMP 计算机上同时运行。 因此，在编写时*CustomDpc*例程，请遵循上一节中规定的准则[注册和队列 DpcForIsr 例程](registering-and-queuing-a-dpcforisr-routine.md)。

 

 




