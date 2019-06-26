---
title: 特定于筛选器的分配器
description: 特定于筛选器的分配器
ms.assetid: 581f3000-4e66-4ba0-979d-b187115a30b2
keywords:
- 筛选器特定的分配器 WDK 内核流式处理
- 筛选器的分配器 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da2183f14a73a53e33369adb37aa5852a44d33a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384056"
---
# <a name="filter-specific-allocators"></a>特定于筛选器的分配器





载入内存或其他设备相关的存储方法要求分配器的筛选器可以通过支持分配器提供特定的分配器[属性](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)并[方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)。 有关详细信息，请参阅[ **KSPROPERTY\_流\_分配器**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)。

筛选器接收 IRP\_MJ\_创建类型 KSCREATE\_请求\_分配器指定分配器的组帧选项。 微型驱动程序的分配器创建例程通过调用来验证创建请求[ **KsValidateAllocatorCreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksvalidateallocatorcreaterequest)。 如果调用成功，此例程返回一个指向相关[ **KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)结构。

如果筛选器不能满足组帧要求，则 IRP 到响应中返回了失败代码。 否则，筛选器将一个指针附加到的结构**FsContext**文件对象和服务的成员生成的分配器请求。

如果缓冲区传递给应修改的流式处理接口的就地筛选器，用户模式下客户端设置 KSALLOCATOR\_REQUIREMENTF\_就地\_上的相关的修饰符标志[ **KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)结构。

有两个接口可供分配器。 首先，所有分配器必须支持基于 IRP [KSMETHODSETID\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)。 使用此机制的分配器被限制为最大的已分配的帧数。 请求分配超过此限制的帧将标记为挂起。

第二，微型驱动程序可以支持函数表访问权限，如果分配池类型可以提供服务在调度\_级别。 提供函数表访问权限是可选的。 执行此操作通过支持中的属性[KSPROPSETID\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)。

调度\_级别接口进行操作，如下所示：

当分配请求提交到分配器时，分配器返回到框架的指针，如果有可用。 如果不是，它立即返回**NULL**。

可用请求提交到分配器，分配器发出信号通知客户端可用的免费的框架，该流的分配器"免费 frame"事件。 此外，如果分配请求正在等待完成的 Irp，分配器必须计划工作项 (如果当前 IRQL 不是被动\_级别) 并完成该请求与免费的框架。

可以为这两个调度\_级别接口和基于 IRP 的接口进行争论免费帧。 KS 同步使用取消自旋锁此队列。

 

 




