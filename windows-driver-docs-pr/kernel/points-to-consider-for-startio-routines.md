---
title: StartIo 例程的注意事项
description: StartIo 例程的注意事项
ms.assetid: 389240d0-682f-48b3-940f-c107e9f60155
keywords:
- StartIo 例程，关于 StartIo 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4f585110db8703aed00f198632b5d26eb8b08a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827669"
---
# <a name="points-to-consider-for-startio-routines"></a>StartIo 例程的注意事项





实现[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程时，请注意以下几点：

-   *StartIo*例程必须将其访问权限同步到物理设备，并将其与驱动程序在设备扩展中维护的任何共享状态信息或资源进行同步，以便访问相同的设备、内存位置或中心.

    如果*StartIo*例程与 ISR 共享设备或状态，则必须使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用驱动程序提供的[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程来对设备进行编程，或访问共享状态。 有关详细信息，请参阅[使用关键部分](using-critical-sections.md)。

    如果*StartIo*例程使用不是 ISR 的例程来共享状态或资源，则必须使用驱动程序为其提供存储的驱动程序初始化的执行自旋锁来保护共享状态或资源。 有关详细信息，请参阅[自旋锁](spin-locks.md)。

-   如果单一的非 WDM 设备驱动程序设置控制器对象，则其*StartIo*例程可以使用控制器对象通过共享的物理设备与附加的（类似）设备同步操作。

    有关详细信息，请参阅[控制器对象](using-controller-objects.md)。

-   基本设备驱动程序的*StartIo*例程必须将大型传输请求拆分到部分传输范围内，才能将大型传输请求拆分到部分传输范围内，并且驱动程序必须执行部分传输设备操作序列。 必须调整每个部分的大小以适合硬件的功能：驱动程序的设备的功能，或对于从属 DMA 设备，还包括系统 DMA 控制器的功能，两者的限制更严格。

    有关使用系统或 bus-主 DMA 的详细信息，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md) 。

-   使用 DMA 的驱动程序的*StartIo*例程必须使用[适配器对象](adapter-objects-and-dma.md)来同步传输。

-   *StartIo*例程以 IRQL = 调度\_级别运行，这会限制它可调用的支持例程集。

    例如， *StartIo*例程既不能访问也不分配可分页内存，也不能等待调度程序对象设置为终止状态。 另一方面， *StartIo*例程可以通过[**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)和[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)获取和释放驱动程序分配的 executive 旋转锁，其运行速度比[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)更快，[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)。

    有关详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)和[旋转锁](spin-locks.md)。

-   如果驱动程序以可取消的状态保存 Irp，则其*StartIo*例程必须检查输入 IRP 是否已被取消，然后才能在其设备上开始处理该请求。 有关详细信息，请参阅[取消 irp](canceling-irps.md)。

 

 




