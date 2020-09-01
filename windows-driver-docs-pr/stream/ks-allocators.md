---
title: KS 分配器
description: KS 分配器
ms.assetid: 07812703-a66f-450a-b28e-4cf765267c4a
keywords:
- 内核流 WDK，分配器
- KS WDK，分配器
- 分配器 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb6e957c2456f9a18b61dc8c4014a1f9db20e22d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189021"
---
# <a name="ks-allocators"></a>KS 分配器





*分配*器是一个 KS 对象，用于实例化被称为 i/o 请求的*帧*的数据缓冲区。 帧是连续内存块区，其大小是通过 KSPIN 描述符的**AllocatorFraming**成员指定的供应商（ [** \_ \_ 例如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

微型驱动程序可以支持多个缓冲区类型的分配器，例如，视频卡中的板上 RAM。 但是，大多数微型驱动程序使用 *默认分配* 器来分配系统内存。 微型驱动程序可以指定帧大小、最大帧数和对齐要求。 默认分配器负责满足要求，并可通过重复使用丢弃的帧来优化性能。

微型驱动程序通过调用 [**KsCreateAllocator**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreateallocator) 例程或相关函数来创建分配器。 在此调用中，微型驱动程序将指针传递到 [**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing) 结构。 此结构包含描述请求的分配器的参数。

在 stream 类模型中，创建分配器的微型驱动程序支持 [**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING**](./ksproperty-connection-allocatorframing.md) 属性。 这是一个只读请求，该请求将返回指向指定接收器句柄相关 [**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing) 结构的指针。

提供分配器的微型驱动程序还应支持 [**KSPROPERTY \_ 流 \_ 分配**](./ksproperty-stream-allocator.md) 器属性。 此属性提供对当前分配给流连接点的分配器的句柄的读/写访问权限。

在 AVStream 下运行的微型驱动程序可能包含实现其自己的分配器的 pin。 通过设置[**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)结构的[**KSALLOCATOR \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksallocator_dispatch)成员来实现此目的。 如果你不想为此 pin 指定分配器，请为此成员指定 **NULL** 。

此外，AVStream 微型驱动程序使用 [**KSALLOCATOR \_ 组帧 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex) 结构来指定分配器要求。 然后，客户端使用 [**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX**](./ksproperty-connection-allocatorframing-ex.md) 属性来检索 pin 的帧需求。 有关详细信息，请参阅 [AVStream 分配器](avstream-allocators.md) 。

本部分包含以下附加信息：

[默认分配器](default-allocators.md)

[特定于筛选器的分配器](filter-specific-allocators.md)

[分配方案](allocation-schemes.md)

 

