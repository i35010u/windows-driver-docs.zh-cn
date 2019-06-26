---
title: AVStream 分配器
description: AVStream 分配器
ms.assetid: cda90faa-d4e3-4f17-aa5a-87dcde314bfd
keywords:
- AVStream 分配器 WDK
- 分配器 WDK AVStream
- 帧 WDK AVStream
- 数据缓冲 WDK AVStream
- 缓冲区 WDK AVStream
- 分配帧 WDK AVStream
- 释放帧 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4396c1322d131155e5494e02111db6af8b8d631
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386708"
---
# <a name="avstream-allocators"></a>AVStream 分配器





AVStream 类驱动程序将使用*Allocator*分配名为的单元中的数据缓冲区*帧*。 框架是连续的内存，它的大小是通过供应商指定的区块**AllocatorFraming**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex).

微型驱动程序访问通过这些缓冲区[Stream 指针](stream-pointers.md)API; 调用[ **KsPinGetLeadingEdgeStreamPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)到流中获取一个指针。

AVStream 客户端可以使用只读属性获取 pin 组帧要求的信息[ **KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing-ex). 此属性返回类型的结构[ **KSALLOCATOR\_组帧\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing_ex) ，用于描述 pin 的组帧要求。

数据不再使用时，AVStream 将使用的分配器释放缓冲区。

AVStream 提供默认分配器。 默认分配器分配基于微型驱动程序中提供的分配器要求的池内存**AllocatorFraming**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。

具有特定于设备的分配要求的供应商可以编写包含其自己的分配例程的微型驱动程序。 例如，你可能会提供一个分配器，如果您的驱动程序分配的内存[常见 DMA 缓冲区](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-common-buffer-system-dma)。

若要提供分配器，提供[ **KSALLOCATOR\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksallocator_dispatch)结构，其中包含指向以下供应商提供的回调例程的指针：

-   [*AVStrMiniInitializeAllocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspininitializeallocator)

-   [*AVStrMiniDeleteAllocator*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdeleteallocator)

-   [*AVStrMiniAllocate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdefaultallocate)

-   [*AVStrMiniAllocatorFreeFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdefaultfree)

提供指向在此分配器调度结构的指针**Allocator**的成员[ **KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)结构描述为其 pin此分配器将实例化框架。

提供指向在此 pin 调度结构的指针**调度**的相应成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 若要了解有关 AVStream 中调度结构的详细信息，请阅读[AVStream 调度表](avstream-dispatch-tables.md)。

在运行时，图形管理器 (例如，[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)模块) 处理的分配器所选内容。 供应商提供的分配器*不*保证供选择的图形管理器。

如果连接是在内核模式下，仅选择内核模式分配器。 此外，如果分配器要求和你的分配器的功能不匹配，则可以拒绝你的分配器。 如果未选择你的分配器，你[ *AVStrMiniInitializeAllocator* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspininitializeallocator)永远不会调用回调例程。

另请参阅[AVStream DMA 服务](avstream-dma-services.md)并[Stream 指针](stream-pointers.md)。

 

 




