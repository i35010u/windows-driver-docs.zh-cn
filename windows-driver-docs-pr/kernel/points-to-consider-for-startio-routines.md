---
title: StartIo 例程的注意事项
description: StartIo 例程的注意事项
keywords:
- StartIo 例程，关于 StartIo 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011581f1760d7ef0b834c79e3c99c7925f74ed76
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822307"
---
# <a name="points-to-consider-for-startio-routines"></a>StartIo 例程的注意事项





实现 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程时，请注意以下几点：

-   *StartIo* 例程必须同步其对物理设备的访问权限，以及与驱动程序在设备扩展中维护的任何共享状态信息或资源，以及访问同一设备、内存位置或资源的驱动程序的其他例程。

    如果 *StartIo* 例程与 ISR 共享设备或状态，则必须使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 调用驱动程序提供的 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程来对设备进行编程，或访问共享状态。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)。

    如果 *StartIo* 例程使用不是 ISR 的例程来共享状态或资源，则必须使用驱动程序为其提供存储的驱动程序初始化的执行自旋锁来保护共享状态或资源。 有关详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md)。

-   如果单一非 WDM 设备驱动程序设置控制器对象，则其 *StartIo* 例程可以使用控制器对象通过连接 (类似) 设备的共享物理设备来同步操作。

    有关详细信息，请参阅 [控制器对象](./introduction-to-controller-objects.md) 。

-   除非紧密耦合的高级驱动程序 presplits 其基础设备驱动程序的大型 DMA 传输请求，否则，基础设备驱动程序的 *StartIo* 例程必须将大型传输请求拆分到部分传输范围内，并且驱动程序必须执行部分传输设备操作序列。 必须调整每个部分的大小以适合硬件的功能：驱动程序的设备的功能，或对于从属 DMA 设备，还包括系统 DMA 控制器的功能，两者的限制更严格。

    有关使用系统或 bus-主 DMA 的详细信息，请参阅 [适配器对象和 DMA](./introduction-to-adapter-objects.md) 。

-   使用 DMA 的驱动程序的 *StartIo* 例程必须使用 [适配器对象](./introduction-to-adapter-objects.md)来同步传输。

-   *StartIo* 例程以 IRQL = 调度 \_ 级别运行，这会限制它可调用的支持例程集。

    例如， *StartIo* 例程既不能访问也不分配可分页内存，也不能等待调度程序对象设置为终止状态。 另一方面， *StartIo* 例程可以通过 [**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) 和 [**KeReleaseSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)获取和释放驱动程序分配的执行旋转锁，其运行速度比 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 和 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)快。

    有关详细信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md) 和 [旋转锁](./introduction-to-spin-locks.md) 。

-   如果驱动程序以可取消的状态保存 Irp，则其 *StartIo* 例程必须检查输入 IRP 是否已被取消，然后才能在其设备上开始处理该请求。 有关详细信息，请参阅 [取消 irp](canceling-irps.md)。

 

