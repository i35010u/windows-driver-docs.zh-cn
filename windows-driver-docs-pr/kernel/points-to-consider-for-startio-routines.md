---
title: 要考虑 StartIo 例程的事项
description: 要考虑 StartIo 例程的事项
ms.assetid: 389240d0-682f-48b3-940f-c107e9f60155
keywords:
- StartIo 例程，有关 StartIo 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d322a35b05940750354b33b42b2970c9e76c066
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369706"
---
# <a name="points-to-consider-for-startio-routines"></a>要考虑 StartIo 例程的事项





在实现时记住以下几点[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程：

-   一个*StartIo*例程必须同步其访问的物理设备和任何共享状态信息或驱动程序保持驱动程序设备扩展插件中的资源的访问同一个设备，内存其他例程位置或资源。

    如果*StartIo*例程与 ISR 共享设备或状态，则必须使用[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)调用驱动程序提供[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)例程进行编程设备或访问共享的状态。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

    如果*StartIo*例程共享状态或具有例程 ISR 以外的资源，它必须保护的共享的状态或具有为其驱动程序提供的存储驱动程序初始化 executive 旋转锁的资源。 有关详细信息，请参阅[旋转锁](spin-locks.md)。

-   如果整体化非 WDM 设备驱动程序设置控制器对象，其*StartIo*例程可以使用控制器对象通过共享物理连接 （类似） 的设备与设备同步操作。

    请参阅[控制器对象](using-controller-objects.md)有关详细信息。

-   除非紧密耦合的更高级别的驱动程序 presplits 大型 DMA 传输请求对于其基础的设备驱动程序，基础设备驱动程序*StartIo*例程必须将大型传输请求拆分为分部传输范围和驱动程序必须执行一系列的部分传输设备操作。 每个部分传输必须将其调整为适合的硬件功能： 功能的驱动程序的设备，或从属的 DMA 设备功能的系统的 DMA 控制器，二者具有更严格的约束。

    请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)有关使用系统或总线 master DMA 详细信息。

-   *StartIo*例程使用 DMA 的驱动程序必须同步使用的传输[适配器对象](adapter-objects-and-dma.md)。

-   一个*StartIo*例程运行在 IRQL = 调度\_级别，限制可以调用的支持例程集。

    例如， *StartIo*例程不能访问或分配可分页内存，并且它不能等待要设置为终止状态的调度程序对象。 但是， *StartIo*例程可以获取和释放使用的驱动程序分配 executive 数值调节钮锁[ **KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)和[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)，它运行速度更快比[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)并[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)。

    请参阅[管理硬件优先级](managing-hardware-priorities.md)并[旋转锁](spin-locks.md)有关详细信息。

-   如果该驱动程序持有 Irp 处于可取消状态，其*StartIo*例程必须检查是否输入的 IRP 已经开始在其设备上请求任何处理之前已取消。 有关详细信息，请参阅[取消 Irp](canceling-irps.md)。

 

 




