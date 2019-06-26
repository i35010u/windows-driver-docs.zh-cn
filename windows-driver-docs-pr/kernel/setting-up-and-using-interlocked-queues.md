---
title: 设置和使用联锁队列
description: 设置和使用联锁队列
ms.assetid: af44a4c0-5aa7-40aa-b511-df95c9bfe9bb
keywords:
- 互锁的 IRP 队列 WDK 内核
- 双向链接的 Irp WDK 内核
- 驱动程序专用线程 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b289a6c08a15cd1dcda5d8992088ec91e364d8e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371249"
---
# <a name="setting-up-and-using-interlocked-queues"></a>设置和使用联锁队列





新的驱动程序应使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)framework 优先于在本部分中所述的方法。

具有设备专用线程的驱动程序或驱动程序使用 executive 工作线程，如大多数系统 FSDs，是要管理其自己运行时内部队列的 Irp 互锁队列中的驱动程序的最有可能类型。 所有的即插即用驱动程序，包括 WDM 驱动程序，还必须某些 Irp 内部排队时使即插即用和电源状态转换。

通常情况下，设置一个双向链接的联锁队列; 这些驱动程序每个 IRP 包含类型的成员[**列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)，该驱动程序可以使用双向链接当前持有 Irp。 如果设置单向链接互锁队列，则驱动程序不能对重试 Irp 中重新排队。

### <a href="" id="ddk-using-an-interlocked-queue-kg"></a>

驱动程序必须设置在设备初始化其互锁队列。 下图说明了双向链接的联锁的队列，驱动程序来设置此类队列，以及一组而必须调用支持例程**ExInterlocked * Xxx*** 驱动程序可以调用以插入到 Irp 和删除从 Irp 的例程队列。

![关系图说明如何使用互锁的队列](images/3intlokq.png)

如此图所示，驱动程序必须存储为队列本身以及提供以下若要设置一个双向链接的联锁队列：

-   该驱动程序必须调用 executive 数值调节钮锁定[ **KeInitializeSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)初始化。 通常情况下，驱动程序初始化自旋锁时设置其设备对象中的设备扩展插件及其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

-   对于队列，该驱动程序必须通过调用初始化列表头[ **InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializelisthead)。

使用双向链接互锁的队列的大多数驱动程序提供必要的存储设备驱动程序创建的设备对象的扩展中。 队列和 executive 自旋锁而是可以位于控制器扩展 (如果该驱动程序使用[控制器对象](using-controller-objects.md)) 或非分页缓冲池分配驱动程序中。

而驱动程序正在接收的 I/O 请求，它可以插入 IRP 到其队列通过调用以下支持例程之一，如果*ListHead*属于类型**列表\_条目**，如中所示上图中：

[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402)将放置在队列末尾的 IRP

[**ExInterlockedInsertHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545397) ，将 IRP 置于队列开头处。 仅当它们必须重试的特定请求时，驱动程序通常会调用该例程。

该驱动程序必须将指针传递到 IRP (*ListEntry*)，因此也*ListHead* executive 自旋锁 (*锁*) 它之前初始化，为每个这些指针**ExInterlockedInsert*Xxx*列表**例程。 仅指向*ListHead*并*锁*驱动程序通过调用取消排队 IRP 时所需[ **ExInterlockedRemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545427). 若要防止死锁，该驱动程序必须不会持续将传递给任何 ExecutiveSpinLock **ExInterlocked * Xxx*** 例程。

互锁的队列受 executive 旋转锁，因为该驱动程序可以其双向链接的队列中插入 Irp，并从正在运行在更短于或等于 IRQL 的任何驱动程序例程以包含多个处理器安全的方式删除它们 = 调度\_级别。

队列使用的类型 ListHead**列表\_条目**上, 图中所示是一个双向链接的列表。 一个具有类型的 ListHead [ **SLIST\_标头**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)是已编序的单向链接列表。 驱动程序已编序的单向链接互锁的队列通过调用初始化 ListHead [ **ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializeslisthead)。

可以使用的驱动程序，永远不会将 I/O 操作重试[ **ExInterlockedPushEntrySList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpushentryslist)并[ **ExInterlockedPopEntrySList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpopentryslist)到管理其队列的 Irp 内部序列化的、 单向链接互锁队列中。 使用此类型互锁任何的队列驱动程序还必须为驻留的存储类型的 ListHead **SLIST\_标头**以及 ExecutiveSpinLock，如中所示[上图](#ddk-using-an-interlocked-queue-kg)。 它必须初始化自旋锁并设置其队列之前调用**ExInterlockedPushEntrySList**要插入到其队列中的第一项。

有关详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)并[旋转锁](spin-locks.md)。 为特定的支持例程的 IRQL 要求，请参阅例程的参考页。

 

 




