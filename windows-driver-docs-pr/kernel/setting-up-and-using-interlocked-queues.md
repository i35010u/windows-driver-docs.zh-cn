---
title: 设置和使用联锁队列
description: 设置和使用联锁队列
ms.assetid: af44a4c0-5aa7-40aa-b511-df95c9bfe9bb
keywords:
- 联锁 IRP 将 WDK 内核排队
- 双重链接的 Irp WDK 内核
- 驱动程序专用线程 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7335fdbbd1d37fe9ef9878e1b8677ac46507616f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838426"
---
# <a name="setting-up-and-using-interlocked-queues"></a>设置和使用联锁队列





新驱动程序应按照本部分中所述的方法优先使用 "[取消安全 IRP 队列](cancel-safe-irp-queues.md)框架"。

具有设备专用线程的驱动程序或使用执行工作线程的驱动程序（如大多数系统 FSDs）是最有可能的驱动程序类型，可用于在联锁队列中管理自己的运行时内部的 Irp 队列。 所有 PnP 驱动程序（包括 WDM 驱动程序）还必须在内部对某些 Irp 进行排队，同时执行 PnP 和电源状态转换。

通常，这些驱动程序设置双向链接的互锁队列;每个 IRP 都包含[**LIST\_ENTRY**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)类型的成员，驱动程序可以使用该成员来连接当前正在持有的链接 irp。 如果某个驱动程序设置了单独链接的联锁队列，则该驱动程序无法重新排队 Irp 进行重试。

### <a href="" id="ddk-using-an-interlocked-queue-kg"></a>

驱动程序必须在设备初始化时设置其联锁队列。 下图说明了双重链接的互锁队列、驱动程序必须调用来设置此类队列的支持例程和一组**ExInterlocked * Xxx*** 例程，驱动程序可以调用此例程将 irp 插入到队列中并从队列中删除 irp。

![说明如何使用联锁队列的图示](images/3intlokq.png)

如图所示，驱动程序必须为队列本身提供存储，并为以下各项设置双向链接的联锁队列：

-   Executive 旋转锁，驱动程序必须调用[**KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)来进行初始化。 通常，当驱动程序为其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中的设备对象设置设备扩展时，驱动程序将初始化自旋锁。

-   队列的列表头，驱动程序必须通过调用[**InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead)进行初始化。

大多数使用双向链接的互锁队列的驱动程序在驱动程序创建的设备对象的设备扩展中提供必要的存储。 队列和执行单元调整锁可以在控制器扩展中（如果驱动程序使用[控制器对象](using-controller-objects.md)），也可以位于由驱动程序分配的非分页池中。

当驱动程序接受 i/o 请求时，它可以通过在*ListHead*的类型为**LIST\_条目**的情况下调用以下任一支持例程，从而将 IRP 插入到其队列中，如下图所示：

[**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)将 IRP 置于队列末尾

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)将 IRP 置于队列的顶层。 驱动程序通常只有在必须重试特定请求时才会调用此例程。

驱动程序必须将指向 IRP （*ListEntry*）的指针以及先前初始化的*ListHead*和 Executive 旋转锁（*锁*）指针传递到其中每个**ExInterlockedInsert*Xxx*列表**例程。 当驱动程序通过调用[**ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)取消排队 IRP 时，只需要指向*ListHead*和*Lock*的指针。 若要防止死锁，驱动程序不得持有传递到任何**ExInterlocked * Xxx*** 例程的 ExecutiveSpinLock。

由于联锁队列受 executive 旋转锁定的保护，因此该驱动程序可以将 Irp 插入到其双重链接队列中，并通过在小于或等于 IRQL = 调度\_级别运行的任何驱动程序例程以多处理器安全的方式将其删除。

ListHead 为**list\_ENTRY**类型的队列，如上图中所示，是双向链接列表。 [ **\_标头**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)类型为 SLIST 的 ListHead 是一个有序的单向链接列表。 驱动程序通过调用[**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)，为有序链接的互锁队列初始化 ListHead。

永远不会重试 i/o 操作的驱动程序可以使用[**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist)和[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist)来管理其在有序、单向链接的互操作队列中的 irp 队列。 使用此类联锁队列的任何驱动程序也必须为类型为**SLIST\_标头**和 ExecutiveSpinLock 的 ListHead 提供常驻存储，如下[图](#ddk-using-an-interlocked-queue-kg)所示。 它必须初始化自旋锁并在调用**ExInterlockedPushEntrySList**之前设置其队列，以将初始条目插入到其队列中。

有关详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)和[旋转锁定](spin-locks.md)。 有关特定支持例程的 IRQL 要求，请参阅例程的参考页。

 

 




