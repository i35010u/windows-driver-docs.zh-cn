---
title: 特定于筛选器的分配器
description: 特定于筛选器的分配器
ms.assetid: 581f3000-4e66-4ba0-979d-b187115a30b2
keywords:
- 筛选特定的分配器 WDK 内核流式处理
- 筛选分配器 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b2dac1763825a42d6ab31b17452bf67405e324a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834390"
---
# <a name="filter-specific-allocators"></a>特定于筛选器的分配器





需要对分配器的内存或其他设备相关存储方法使用的筛选器可以通过支持分配器[属性](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)和[方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)来提供特定分配器。 有关详细信息，请参阅[**KSPROPERTY\_STREAM\_分配**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)器。

筛选器接收 IRP\_MJ\_CREATE of KSCREATE\_REQUEST\_分配器指定分配器的组帧选项。 微型驱动程序的分配器创建例程通过调用[**KsValidateAllocatorCreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksvalidateallocatorcreaterequest)来验证创建请求。 如果调用成功，则此例程返回指向相关[**KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)结构的指针。

如果筛选器无法满足组帧要求，它将返回失败代码以响应 IRP。 否则，筛选器会将指向结构的指针附加到 file 对象的**FsContext**成员，并为生成的分配器请求服务。

如果筛选器应就地修改传递到流式处理接口的缓冲区，则用户模式客户端会将相关 KSALLOCATOR 上的 KSALLOCATOR\_REQUIREMENTF\_就地\_修饰符标志设置为[ **\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)构造.

分配器提供两个接口。 首先，所有分配器必须支持基于 IRP 的[KSMETHODSETID\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)。 使用此机制的分配器限制为分配的最大帧数。 分配超出此限制的帧的请求将被标记为 "挂起"。

其次，如果可以在调度\_级别提供分配池类型，则微型驱动程序可以支持函数表访问。 提供函数表访问是可选的。 为此，请支持[KSPROPSETID\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)中的属性。

调度\_级别接口的操作如下所示：

当向分配器提交分配请求时，分配器会返回一个指向帧的指针（如果有）。 否则，它会立即返回**NULL**。

向分配器提交免费请求时，分配器会向流分配器发送 "自由帧" 事件，通知客户端有可用的帧。 此外，如果存在等待完成的分配请求 Irp，则分配器必须计划辅助角色项目（如果当前 IRQL 不是被动\_级别）并使用自由帧完成请求。

调度\_级别接口和基于 IRP 的接口可能会争用自由帧。 KS 使用取消旋转锁来同步此队列。

 

 




