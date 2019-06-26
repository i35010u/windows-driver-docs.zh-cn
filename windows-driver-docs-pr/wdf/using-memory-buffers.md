---
title: 使用内存缓冲区
description: 使用内存缓冲区
ms.assetid: f5699837-f1ba-4088-82b3-d7e27341fb46
keywords:
- 内存缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
- 内存对象 WDK KMDF
- framework 对象 WDK KMDF，内存对象
- 后备链列出 WDK KMDF
- 内存描述符列出 WDK KMDF
- MDLs WDK KMDF
- WDK KMDF 的本地缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c74e631612ba02c1187d3e5f10d9d0ddc31ec5d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372226"
---
# <a name="using-memory-buffers"></a>使用内存缓冲区





驱动程序通常使用内存缓冲区，以将数据传入和从框架和其他驱动程序或存储本地信息。 本主题介绍[framework 内存对象](#using-framework-memory-objects)，[后备链列表](#using-lookaside-lists)， [MDLs](#using-mdls)，以及[本地缓冲区](#allocating-local-buffers)。

### <a href="" id="using-framework-memory-objects"></a> 使用 Framework 内存对象

框架将使用*内存对象*来描述驱动程序从接收，并将传递到框架的内存缓冲区。 每个 framework 内存对象表示一个缓冲区。

若要创建内存对象，您的驱动程序调用以下对象方法之一：

-   [**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)，创建一个内存对象，并分配指定大小的内存缓冲区。

-   [**WdfMemoryCreatePreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)，这将创建预先分配的缓冲区的内存对象。

-   [**WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)，这将创建从内存缓冲区[后备](#using-lookaside-lists)。

若要获取一个表示已接收的 I/O 请求的内存对象进行缓冲，驱动程序调用[ **WdfRequestRetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)并[ **WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)。 检索的 I/O 请求的缓冲区的详细信息，请参阅[基于 Framework 的驱动程序中访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

若要获取的地址和内存对象的缓冲区的大小，您的驱动程序调用[ **WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)。

若要将数据移入或移出内存对象的缓冲区，您的驱动程序调用任一[ **WdfMemoryCopyFromBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)或[ **WdfMemoryCopyToBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer). 这些对象的方法检查源和目标的大小，并防止缓冲区溢出错误。

如果您的驱动程序通过调用创建的内存对象[ **WdfMemoryCreatePreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)，它随后可以将不同的缓冲区通过调用分配给内存对象[ **WdfMemoryAssignBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)。

当驱动程序发送的 I/O 请求[I/O 目标](using-i-o-targets.md)，它通常将传递到的输入或输出缓冲区[framework I/O 目标对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/)。 该驱动程序通过任一传入指定的缓冲区[ **WDF\_内存\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)结构描述缓冲区或通过将内存对象传入处理。 (同步发送的 I/O 请求的 I/O 目标对象方法需要**WDF\_内存\_描述符**结构和发送的 I/O 请求以异步方式需要的内存对象句柄的方法。)

有关内存缓冲区时有效的信息，请参阅[内存缓冲区生命周期](memory-buffer-life-cycle.md)。

### <a href="" id="using-lookaside-lists"></a> 使用后备链列表

如果您的驱动程序将要求多的缓冲区大小大约相同的它应分配从*后备*。 该驱动程序通过调用创建后备链列表[ **WdfLookasideListCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdflookasidelistcreate)。 随后，该驱动程序可以获取缓冲区从后备链列表通过调用[ **WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)。

每次驱动程序调用[ **WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)，框架将创建内存对象，从后备链列表中，获取缓冲区和将缓冲区分配给对象。 该驱动程序结束时使用它将调用这些内存对象之一[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)，它删除内存对象并返回缓冲区空间的到后备链列表。

操作系统管理分配给后备链列表的内存资源。 如果该驱动程序从后备链列表请求缓冲区时均不可用，例如驱动程序调用的第一个时间[ **WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)，系统将分配一个缓冲区，并将其分配到列表中。 当驱动程序调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) （和缓冲区空间返回到后备链列表），系统在列表中保留现在未分配的缓冲区，直到该驱动程序再次需要。 系统会增加为必需的; 此列表的大小例如，更频繁地请求缓冲区接收可查看大后备链列表的驱动程序。 另一方面，如果驱动程序不使用所有这些系统，就可能会降低在列表中的缓冲区数。

### <a href="" id="using-mdls"></a> 使用 MDLs

某些驱动程序使用描述符列出 (MDLs) 来描述缓冲区的内存。 例如，直接内存访问 (DMA) 设备的驱动程序必须将传递到 MDL [ **WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)方法时，如果它调用该方法。

使用 MDLs 的驱动程序可以获取通过调用表示已接收的 I/O 请求的缓冲区 MDL [ **WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)并[ **WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)。

大多数基于框架的驱动程序不使用 MDLs。

### <a href="" id="allocating-local-buffers"></a> 分配的本地缓冲区

驱动程序需要它不会传递到框架的本地的内部缓冲区空间，无需创建内存对象来表示缓冲区。 该驱动程序可以调用[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)分配内部缓冲区。 完成后使用的缓冲区的驱动程序，它必须调用[ **ExFreePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag)。

但是，驱动程序还可以使用内存对象的本地缓冲区。 使用内存缓冲区，而不调用优势[ **ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)，是，框架将自动删除内存对象和其缓冲区每个对象的父对象时已删除。

### <a name="aligning-buffers"></a>对齐缓冲区

可以使用您的驱动程序[ **WDF\_对齐\_大小\_向上**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcore/nf-wdfcore-wdf_align_size_up)或[ **WDF\_对齐\_大小\_向下**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcore/nf-wdfcore-wdf_align_size_down)函数来计算指定的对齐方式偏移量为对齐的缓冲区大小。 如果每个缓冲区必须在地址对齐边界处开始，此计算非常有用，如果您的驱动程序必须分配多个连续缓冲区。

 

 





