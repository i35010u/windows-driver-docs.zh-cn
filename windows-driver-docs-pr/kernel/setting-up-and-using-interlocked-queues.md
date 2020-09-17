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
ms.openlocfilehash: c21f4ffbe84d09e54f9dccb0a95e20ef2d7eec16
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717480"
---
# <a name="setting-up-and-using-interlocked-queues"></a>设置和使用联锁队列





新驱动程序应按照本部分中所述的方法优先使用 " [取消安全 IRP 队列](cancel-safe-irp-queues.md) 框架"。

具有设备专用线程的驱动程序或使用执行工作线程的驱动程序（如大多数系统 FSDs）是最有可能的驱动程序类型，可用于在联锁队列中管理自己的运行时内部的 Irp 队列。 所有 PnP 驱动程序（包括 WDM 驱动程序）还必须在内部对某些 Irp 进行排队，同时执行 PnP 和电源状态转换。

通常，这些驱动程序设置双向链接的互锁队列;每个 IRP 都包含类型为 [**LIST \_ 条目**](/windows/win32/api/ntdef/ns-ntdef-_list_entry)的成员，驱动程序可以使用该成员来连接当前正在持有的链接 irp。 如果某个驱动程序设置了单独链接的联锁队列，则该驱动程序无法重新排队 Irp 进行重试。

### <a href="" id="ddk-using-an-interlocked-queue-kg"></a>

驱动程序必须在设备初始化时设置其联锁队列。 下图说明了双重链接的互锁队列、驱动程序必须调用来设置此类队列的支持例程和一组 **ExInterlocked * Xxx*** 例程，驱动程序可以调用此例程将 irp 插入到队列中并从队列中删除 irp。

![说明如何使用联锁队列的图示](images/3intlokq.png)

如图所示，驱动程序必须为队列本身提供存储，并为以下各项设置双向链接的联锁队列：

-   Executive 旋转锁，驱动程序必须调用 [**KeInitializeSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock) 来进行初始化。 通常，当驱动程序为其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中的设备对象 () 设置设备)  (扩展时，驱动程序将初始化自旋锁。

-   队列的列表头，驱动程序必须通过调用 [**InitializeListHead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead)进行初始化。

大多数使用双向链接的互锁队列的驱动程序在驱动程序创建的设备对象的设备扩展中提供必要的存储。 如果驱动程序使用 [控制器对象](./introduction-to-controller-objects.md)) 或由驱动程序分配的非分页池，则队列和执行单元旋转锁定可以是在控制器扩展 (。

当驱动程序接受 i/o 请求时，它可以通过在 *ListHead* 的类型为 **LIST \_ 条目**的情况下调用以下任一支持例程，从而将 IRP 插入到其队列中：

[**ExInterlockedInsertTailList**](/previous-versions/ff545402(v=vs.85)) 将 IRP 置于队列末尾

[**ExInterlockedInsertHeadList**](/previous-versions/ff545397(v=vs.85)) 将 IRP 置于队列的顶层。 驱动程序通常只有在必须重试特定请求时才会调用此例程。

驱动程序必须将指向 IRP (*ListEntry*) 的指针传递给 IRP，还必须将 *ListHead* 和 Executive 旋转锁定 (*锁*) 之前初始化的指针）传递给每个 **ExInterlockedInsert*Xxx*列表** 例程。 当驱动程序通过调用[**ExInterlockedRemoveHeadList**](/previous-versions/ff545427(v=vs.85))取消排队 IRP 时，只需要指向*ListHead*和*Lock*的指针。 若要防止死锁，驱动程序不得持有传递到任何 **ExInterlocked * Xxx*** 例程的 ExecutiveSpinLock。

由于联锁队列由执行单元旋转锁定进行保护，因此该驱动程序可以将 Irp 插入其双重链接队列中，并从运行时间小于或等于 IRQL = 调度级别的任何驱动程序例程以多处理器安全的方式将其删除 \_ 。

如上图所示，具有 ListHead 类型 **列表 \_ 项**的队列是双重链接列表。 具有 [**SLIST \_ 标头**](./eprocess.md) 类型的 ListHead 的是一个有序的单向链接列表。 驱动程序通过调用 [**ExInitializeSListHead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)，为有序链接的互锁队列初始化 ListHead。

永远不会重试 i/o 操作的驱动程序可以使用 [**ExInterlockedPushEntrySList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist) 和 [**ExInterlockedPopEntrySList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist) 来管理其在有序、单向链接的互操作队列中的 irp 队列。 使用此类联锁队列的任何驱动程序也必须为 **SLIST \_ 标头** 和 ExecutiveSpinLock 类型的 ListHead 提供常驻存储，如下 [图](#ddk-using-an-interlocked-queue-kg)所示。 它必须初始化自旋锁并在调用 **ExInterlockedPushEntrySList** 之前设置其队列，以将初始条目插入到其队列中。

有关详细信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md) 和 [旋转锁定](./introduction-to-spin-locks.md)。 有关特定支持例程的 IRQL 要求，请参阅例程的参考页。

 

