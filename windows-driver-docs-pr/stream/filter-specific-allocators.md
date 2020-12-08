---
title: 特定于筛选器的分配器
description: 特定于筛选器的分配器
keywords:
- 筛选特定的分配器 WDK 内核流式处理
- 筛选分配器 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8791f16b13d38ec54e08b18eaf8c3eb9b0649912
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839975"
---
# <a name="filter-specific-allocators"></a>特定于筛选器的分配器





需要对分配器的内存或其他设备相关存储方法使用的筛选器可以通过支持分配器 [属性](./kspropsetid-streamallocator.md) 和 [方法](./ksmethodsetid-streamallocator.md)来提供特定分配器。 有关详细信息，请参阅 [**KSPROPERTY \_ 流 \_ 分配**](./ksproperty-stream-allocator.md)器。

筛选器将接收 \_ \_ 类型为 KSCREATE 请求分配器的 IRP MJ 创建，并 \_ \_ 指定分配器的组帧选项。 微型驱动程序的分配器创建例程通过调用 [**KsValidateAllocatorCreateRequest**](/windows-hardware/drivers/ddi/ks/nf-ks-ksvalidateallocatorcreaterequest)来验证创建请求。 如果调用成功，则此例程返回指向相关 [**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing) 结构的指针。

如果筛选器无法满足组帧要求，它将返回失败代码以响应 IRP。 否则，筛选器会将指向结构的指针附加到 file 对象的 **FsContext** 成员，并为生成的分配器请求服务。

如果筛选器应就地修改传递到流式处理接口的缓冲区，则用户模式客户端将 \_ \_ \_ 在相关 [**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing) 结构上设置 KSALLOCATOR REQUIREMENTF 就地修饰符标志。

分配器提供两个接口。 首先，所有分配器必须支持基于 IRP 的 [KSMETHODSETID \_ StreamAllocator](./ksmethodsetid-streamallocator.md)。 使用此机制的分配器限制为分配的最大帧数。 分配超出此限制的帧的请求将被标记为 "挂起"。

其次，如果可以在调度级别为分配池类型提供服务，微型驱动程序可以支持函数表访问 \_ 。 提供函数表访问是可选的。 为此，请支持 [KSPROPSETID \_ StreamAllocator](./kspropsetid-streamallocator.md)中的属性。

调度 \_ 级别接口的操作如下所示：

当向分配器提交分配请求时，分配器会返回一个指向帧的指针（如果有）。 否则，它会立即返回 **NULL**。

向分配器提交免费请求时，分配器会向流分配器发送 "自由帧" 事件，通知客户端有可用的帧。 此外，如果存在等待完成的分配请求 Irp，则分配器必须计划辅助角色项 (如果当前 IRQL 不是被动 \_ 级别) 并使用自由帧完成请求。

调度 \_ 级别接口和基于 IRP 的接口可能会争用自由帧。 KS 使用取消旋转锁来同步此队列。

 

