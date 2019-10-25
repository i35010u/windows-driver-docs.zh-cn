---
title: CLFS 封送区域
description: CLFS 封送区域
ms.assetid: 1153bcfd-43e9-43bd-b893-5ec044ea9584
keywords:
- 公用日志文件系统 WDK 内核，封送处理区
- CLFS WDK 内核，封送区
- 封送区 WDK CLFS
- 日志 i/o 缓冲区 WDK CLFS
- 最大日志 i/o 缓冲区数 WDK CLFS
- 内存分配 WDK CLFS
- 缓冲区 WDK CLFS
- 追加记录 WDK CLFS
- 稳定存储 WDK CLFS
- 可变内存 WDK CLFS
- 存储 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b3c0cae27f87d91ba4a251337406ebdb1dff8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828539"
---
# <a name="clfs-marshalling-areas"></a>CLFS 封送区域





公用日志文件系统（CLFS）客户端将日志记录追加到易失内存中的[*封送处理区域*](clfs-terminology.md#kernel-clfs-term-marshalling-area)，CLFS 会定期将这些记录写入稳定的存储。 封送处理区域是日志 i/o 缓冲区的集合，其中每个缓冲区都可以包含多个日志记录。 日志 i/o 缓冲区将最近写入到流中的记录（但可能未刷新到稳定存储）以及最近从流中读取的记录保留。

您可以通过调用[**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)创建一个封送处理区，此时您必须指定该封送处理区将使用的日志 i/o 缓冲区的大小，以及这些缓冲区是在分页或非分页池中。 封送处理区中的所有日志 i/o 缓冲区大小相同，CLFS 可确保大小为底层稳定存储介质上的扇区大小的倍数。 也就是说，CLFS 将获得您请求的大小并根据需要对其进行舍入，使 i/o 缓冲区与稳定存储介质兼容。

CLFS 根据需要分配并释放日志 i/o 缓冲区，但你可以选择设置一次可以分配的最大 i/o 缓冲区数。 你还可以选择提供自己的缓冲区分配和释放函数。

若要指定一次可以分配用于写入日志记录的最大日志 i/o 缓冲区数，请设置**ClfsCreateMarshallingArea**函数的*cMaxWriteBuffers*参数。 限制缓冲区数量会影响刷新对稳定存储的频率;如果缓冲区较少，则必须更频繁地将日志记录写入稳定的存储。 如果不需要控制刷新频率，请将*cMaxWriteBuffers*设置为无限大（在 winbase.h 中定义）。

若要指定一次可以分配以读取日志记录的最大日志 i/o 缓冲区数，请设置**ClfsCreateMarshallingArea**函数的*cMaxReadBuffers*参数。 如果不需要控制分配的读取缓冲区的数目，请将*cMaxReadBuffers*设置为无限大。

如果要对日志 i/o 缓冲区进行自己的内存分配，请设置**ClfsCreateMarshallingArea**函数的*pfnAllocBuffer*和*pfnFreeBuffer*参数，使其指向你自己的分配和释放函数。 然后，CLFS 将调用函数，以便在需要创建或释放日志 i/o 缓冲区时执行实际的内存分配和释放。

在某些情况下，可能需要提前在封送处理区域中保留空间。 例如，您可能知道您要编写一组10个日志记录，并且您希望确保在封送区中有足够的空间用于整个集。 若要为10个记录保留空间，请创建一个包含记录大小的十元素数组，然后将该数组传递给*rgcbReservation*参数中的[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)函数。 **ClfsReserveAndAppendLog**是一种多用途功能，它在封送区中保留空间，或将日志记录追加到流或以原子方式执行这两项任务。 通过适当地设置参数，可以调用**ClfsReserveAndAppendLog**来保留空间供将来使用，而无需将任何记录实际追加到流中。

 

 




