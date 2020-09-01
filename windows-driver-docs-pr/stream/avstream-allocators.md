---
title: AVStream 分配器
description: AVStream 分配器
ms.assetid: cda90faa-d4e3-4f17-aa5a-87dcde314bfd
keywords:
- AVStream 分配器 WDK
- 分配器 WDK AVStream
- 帧 WDK AVStream
- 数据缓冲区 WDK AVStream
- 缓冲区 WDK AVStream
- 分配帧 WDK AVStream
- 释放帧 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16ec4623edfc5250056e544d4148b1788e69793a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192881"
---
# <a name="avstream-allocators"></a>AVStream 分配器





AVStream 类驱动程序使用 *分配* 器在名为 *帧*的单元中分配数据缓冲区。 帧是连续内存块区，其大小是通过 KSPIN 描述符的**AllocatorFraming**成员指定的供应商（ [** \_ \_ 例如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

微型驱动程序通过 [流指针](stream-pointers.md) API 访问这些缓冲区;调用 [**KsPinGetLeadingEdgeStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer) 以获取指向流的指针。

AVStream 客户端可以通过使用只读属性 [**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX**](./ksproperty-connection-allocatorframing-ex.md)获取有关 pin 的帧需求的信息。 此属性返回 [**KSALLOCATOR \_ 组帧 \_ **](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex) 的类型的结构，其中描述了 pin 的组帧要求。

当不再使用数据时，AVStream 将使用分配器来释放缓冲区。

AVStream 提供默认分配器。 默认分配器根据微型驱动程序在[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的**AllocatorFraming**成员中提供的分配器要求，分配池内存。

具有特定于设备的分配要求的供应商可以编写包含其自己的分配例程的微型驱动程序。 例如，如果驱动程序从 [公共 DMA 缓冲区](../kernel/using-common-buffer-system-dma.md)分配内存，则可以提供分配器。

若要提供分配器，请提供 [**KSALLOCATOR \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksallocator_dispatch) 结构，该结构包含指向以下供应商提供的回调例程的指针：

-   [*AVStrMiniInitializeAllocator*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspininitializeallocator)

-   [*AVStrMiniDeleteAllocator*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdeleteallocator)

-   [*AVStrMiniAllocate*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdefaultallocate)

-   [*AVStrMiniAllocatorFreeFrame*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdefaultfree)

提供一个指针，该指针指向用于描述此分配器将为其实例化帧的 pin 的[**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)结构的**分配**器成员中的此分配器调度结构。

提供一个指针，该指针指向相应[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的**调度**成员。 若要详细了解 AVStream 中的调度结构，请阅读 [AVStream 调度表](avstream-dispatch-tables.md)。

在运行时，图形管理器 (例如， [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index) 模块) 处理分配器选择。 *不*保证关系图管理器选择供应商提供的分配器。

仅当连接处于内核模式时，才会选择内核模式分配器。 此外，如果分配器要求和分配器的功能不匹配，则分配器可能会被拒绝。 如果未选择分配器，则永远不会调用 [*AVStrMiniInitializeAllocator*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspininitializeallocator) 回调例程。

另请参阅 [AVSTREAM DMA 服务](avstream-dma-services.md) 和 [流指针](stream-pointers.md)。

 

