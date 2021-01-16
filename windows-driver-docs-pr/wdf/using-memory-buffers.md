---
title: 使用内存缓冲区
description: 使用内存缓冲区
keywords:
- 内存缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
- 内存对象 WDK KMDF
- framework 对象 WDK KMDF，内存对象
- 后备链表列出 WDK KMDF
- 内存描述符列出 WDK KMDF
- MDLs WDK KMDF
- 本地缓冲区 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46a91372cb3900925f4aa3b8fa24d94d12d2c730
ms.sourcegitcommit: dbf5b780975d2911545d8bfa6fead4a97e7cfa88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2021
ms.locfileid: "98248250"
---
# <a name="using-memory-buffers"></a>使用内存缓冲区





驱动程序通常使用内存缓冲区向/从框架及其他驱动程序传入数据，或在本地存储信息。 本主题介绍 [framework memory 对象](#using-framework-memory-objects)、 [后备链表列表](#using-lookaside-lists)、 [MDLs](#using-mdls)和 [本地缓冲区](#allocating-local-buffers)。

### <a name="using-framework-memory-objects"></a><a href="" id="using-framework-memory-objects"></a> 使用 Framework 内存对象

框架使用 *内存对象* 来描述驱动程序从其接收并传递到框架的内存缓冲区。 每个 framework memory 对象表示一个缓冲区。

若要创建内存对象，驱动程序将调用以下对象方法之一：

-   [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)，它创建内存对象，并分配指定大小的内存缓冲区。

-   [**WdfMemoryCreatePreallocated**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)，它为预先分配的缓冲区创建内存对象。

-   [**WdfMemoryCreateFromLookaside**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)，它从 [后备链表列表](#using-lookaside-lists)创建内存缓冲区。

若要获取表示接收到的 i/o 请求缓冲区的内存对象，驱动程序将调用 [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 和 [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)。 有关检索 i/o 请求的缓冲区的详细信息，请参阅 [访问 Framework-Based 驱动程序中的数据缓冲区](./accessing-data-buffers-in-wdf-drivers.md)。

若要获取内存对象缓冲区的地址和大小，驱动程序将调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)。

若要将数据移入或移出内存对象的缓冲区，驱动程序可以调用 [**WdfMemoryCopyFromBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 或 [**WdfMemoryCopyToBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)。 这些对象方法检查源和目标的大小，并防止缓冲区溢出错误。

如果驱动程序通过调用 [**WdfMemoryCreatePreallocated**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)来创建内存对象，则可以通过调用 [**WdfMemoryAssignBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)为内存对象分配不同的缓冲区。

当驱动程序向 [i/o 目标](using-i-o-targets.md)发送 i/o 请求时，它通常会将输入或输出缓冲区传递到 [框架 i/o 目标对象方法](/windows-hardware/drivers/ddi/wdfiotarget/)。 驱动程序通过传递描述缓冲区的 [**WDF \_ 内存 \_ 描述符**](/windows-hardware/drivers/ddi/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor) 结构或通过传递内存对象句柄来指定缓冲区。  (发送 i/o 请求的 i/o 目标对象方法需要一个 **WDF \_ 内存 \_ 描述符** 结构，并且异步发送 i/o 请求的方法需要内存对象句柄。 ) 

有关内存缓冲区有效的详细信息，请参阅 [内存缓冲区生命周期](memory-buffer-life-cycle.md)。

### <a name="using-lookaside-lists"></a><a href="" id="using-lookaside-lists"></a> 使用后备链表列表

如果你的驱动程序需要的多个缓冲区大小大致相同，应从 *后备链表列表* 中进行分配。 驱动程序通过调用 [**WdfLookasideListCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdflookasidelistcreate)创建后备链表列表。 随后，驱动程序可以通过调用 [**WdfMemoryCreateFromLookaside**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)从后备链表列表中获取缓冲区。

每次驱动程序调用 [**WdfMemoryCreateFromLookaside**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)时，框架都将创建一个内存对象，从后备链表列表中获取一个缓冲区，并将该缓冲区分配给该对象。 当驱动程序使用完其中一个内存对象时，它将调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)，这将删除内存对象并将缓冲区空间返回到后备链表列表。

操作系统管理分配给后备链表列表的内存资源。 如果驱动程序在没有可用的情况下从后备链表列表请求缓冲区，例如，当驱动程序第一次调用 [**WdfMemoryCreateFromLookaside**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)时，系统将分配一个缓冲区并将其分配给列表。 当驱动程序调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) (并将缓冲区空间返回到后备链表列表时) ，系统将在列表中保留现在未分配的缓冲区，直到驱动程序再次需要该缓冲区。 系统会根据需要增加列表的大小;例如，更频繁请求缓冲区的驱动程序将接收更大的后备链表列表。 另一方面，如果驱动程序没有使用它们，系统可以减少列表中的缓冲区数。

### <a name="using-mdls"></a><a href="" id="using-mdls"></a> 使用 MDLs

某些驱动程序使用内存描述符列表 (MDLs) 描述缓冲区。 例如，如果 (DMA) 设备的直接内存访问的驱动程序调用该方法，则必须将 MDL 传递到 [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 方法。

使用 MDLs 的驱动程序可以通过调用 [**WdfRequestRetrieveInputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) 和 [**WdfRequestRetrieveOutputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)获取表示已接收 i/o 请求的缓冲区的 MDL。

大多数基于框架的驱动程序不使用 MDLs。

### <a name="allocating-local-buffers"></a><a href="" id="allocating-local-buffers"></a> 分配本地缓冲区

需要本地的内部缓冲区空间的驱动程序不会传递到框架，无需创建内存对象来表示缓冲区。 驱动程序可以调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 来分配内部缓冲区。 当驱动程序使用完缓冲区后，必须调用 [**ExFreePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)。

但是，驱动程序还可以将内存对象用于本地缓冲区。 使用内存缓冲区（而不是调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)）的优点在于，当删除每个对象的父对象时，框架会自动删除内存对象及其缓冲区。

>[!IMPORTANT]
> 本主题中讨论的 ExAllocatePool DDIs 已在 Windows 10 版本2004中弃用，并且已被 [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) 和 [ExAllocatePool3](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool3)替换。 有关详细信息，请参阅 [将弃用的 ExAllocatePool 调用更新到 ExAllocatePool2 和 ExAllocatePool3](/windows-hardware/drivers/kernel/updating-deprecated-exallocatepool-calls)。

### <a name="aligning-buffers"></a>对齐缓冲区

你的驱动程序可以使用 " [**wdf \_ 对齐 \_ 大小 \_**](/windows-hardware/drivers/ddi/wdfcore/nf-wdfcore-wdf_align_size_up) " 或 " [**wdf 调整 \_ \_ 大小 \_**](/windows-hardware/drivers/ddi/wdfcore/nf-wdfcore-wdf_align_size_down) " 功能来计算与指定的对齐偏移量对齐的缓冲区大小。 如果你的驱动程序必须在地址对齐边界开始时分配多个连续缓冲区，则此计算非常有用。

 

