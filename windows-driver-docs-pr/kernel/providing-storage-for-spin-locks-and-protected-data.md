---
title: 为自旋锁和受保护数据提供存储
description: 为自旋锁和受保护数据提供存储
ms.assetid: bde18474-10c3-4d9a-b120-6cbd5fc675cc
keywords:
- 存储 WDK 旋转锁
- 存储旋转锁定保护的数据
- 旋转锁定 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9ef5b57673eaa2965ae18a4324731cc7003b89
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184429"
---
# <a name="providing-storage-for-spin-locks-and-protected-data"></a>为自旋锁和受保护数据提供存储





在设备启动过程中，驱动程序必须为任何旋转锁定保护的数据或资源分配驻留存储，并在以下任一位置为相应的自旋锁分配存储：

-   驱动程序通过调用 IoCreateDevice 设置的设备对象的设备扩展[ **IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

-   驱动程序通过调用 IoCreateController 设置的控制器对象的控制器扩展[ **IoCreateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)

-   未分页，驱动程序通过调用 ExAllocatePoolWithTag 获取的系统空间[ **ExAllocatePoolWithTag**内存](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

如果尝试在持有自旋锁时访问可分页数据，则会导致出现严重页面错误（如果该页不存在）。 引用 (无效的旋转锁，因为它存储在可分页内存中并且当前已分页) 也会导致严重页错误。

驱动程序必须为其可能使用的以下各种类型的执行旋转锁定提供存储：

- 驱动程序使用任何 **Ke * Xxx*** 自旋锁例程显式获取和释放的任何自旋锁。

- 任何用作 **ExInterlocked * Xxx*** 例程的参数的自旋锁。

尽管驱动程序可以调用其 ISR 或[*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程中的**ExInterlocked * xxx*** 例程，但它不能使用任何**Ke * xxx*** 例程来获取和释放大于调度级别的任何 IRQL 处的自旋锁 \_ 。 因此，在对 **Ke*Xxx*旋转锁** 和 **ExInterlocked * Xxx*** 例程的调用之间重复使用自旋锁的任何驱动程序都必须在 IRQL &lt; = 调度级别运行时进行每个调用 \_ 。

只要两个例程在相同的 IRQL 上使用自旋锁，驱动程序就可以将相同的旋转锁定传递到 **ExInterlockedInsertHeadList** ，就像处理另一 **ExInterlocked * Xxx*** 例程一样。 有关自旋锁使用如何影响性能的详细信息，请参阅 [使用自旋锁：一个示例](using-spin-locks--an-example.md)。

除了对其执行单元旋转锁的存储之外，设备驱动程序还必须为要与其中断对象关联的另一个自旋锁（如果它具有 multivector ISR 或多个 ISR）提供存储。

 

