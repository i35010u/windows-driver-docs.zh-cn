---
title: KS 分配器
description: KS 分配器
ms.assetid: 07812703-a66f-450a-b28e-4cf765267c4a
keywords:
- 流式处理 WDK，分配器的内核
- KS WDK，分配器
- 流式处理的分配器 WDK 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323d0433528d7d9f93e728adbe7f14b999b5b535
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382536"
---
# <a name="ks-allocators"></a>KS 分配器





*Allocator*称为实例化数据缓冲区的 KS 对象*帧*的 I/O 请求。 框架是连续的内存，它的大小是通过供应商指定的区块**AllocatorFraming**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex).

微型驱动程序可以支持分配器的多个缓冲区类型，例如板载 RAM 中的视频卡。 但是，大多数微型驱动程序使用*默认分配器*来分配系统内存。 帧大小、 最大数量的帧和对齐要求，可以指定微型驱动程序。 默认分配器负责满足要求，并可能通过重复使用已丢弃的帧来优化性能。

微型驱动程序通过调用创建一个分配器[ **KsCreateAllocator** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreateallocator)例程或相关的函数。 在此调用，微型驱动程序将传递一个指向[ **KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)结构。 此结构包含描述所请求的分配器参数。

在流类模型中，创建的分配器的微型驱动程序支持[ **KSPROPERTY\_连接\_ALLOCATORFRAMING** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing)属性。 这是只读的请求返回一个指向相关[ **KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)为指定的接收器句柄的结构。

提供的分配器的微型驱动程序还应支持[ **KSPROPERTY\_流\_分配器**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)属性。 此属性提供对当前已分配给流连接点的分配器的句柄的读/写访问。

AVStream 下运行的微型驱动程序可能包括实现其自己的分配器的 pin。 执行此操作通过设置[ **KSALLOCATOR\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksallocator_dispatch)隶属[ **KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)结构. 指定**NULL**为此成员，如果不想指定此 pin 的分配器。

此外，使用 AVStream 微型驱动程序[ **KSALLOCATOR\_组帧\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing_ex)结构，以指定分配器要求。 然后使用客户端[ **KSPROPERTY\_连接\_ALLOCATORFRAMING\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing-ex)属性来检索组帧 pin 的要求。 请参阅[AVStream 分配器](avstream-allocators.md)有关详细信息。

本部分包含以下附加信息：

[默认分配器](default-allocators.md)

[筛选器特定分配器](filter-specific-allocators.md)

[分配方案](allocation-schemes.md)

 

 




