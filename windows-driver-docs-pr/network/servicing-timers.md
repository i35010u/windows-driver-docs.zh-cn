---
title: 服务计时器
description: 服务计时器
ms.assetid: 6a80a55b-4c7e-4a48-8903-0a1fb28af153
keywords:
- timer 服务 WDK NDIS
- NDIS timer 服务 WDK
- 取消 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f80430f096912d1ebbc7fa3bc51db18fab20d0a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216082"
---
# <a name="servicing-timers"></a>服务计时器





当 NDIS 6.0 计时器触发时，NDIS 将调用 [**NetTimerCallback**](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function) 函数。 此函数的 *FunctionContext* 参数包含指向驱动程序提供的上下文区域的指针。 *FunctionContext*的默认值是在[**NDIS \_ 计时器 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_timer_characteristics)结构中指定的。 驱动程序将结构传递到 [**NdisAllocateTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject) 函数，以分配和初始化关联的计时器对象。

如果驱动程序在传递到[**NdisSetTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)函数的*FunctionContext*参数中指定了非 NULL 值，则 NDIS 会将该值传递给*NetTimerCallback*函数的*FunctionContext*参数。 否则，NDIS 会传递在 NDIS \_ 计时器特征结构中指定的默认值 \_ 。

任何 NDIS 驱动程序都可以有多个 *NetTimerCallback* 函数。 每个此类 *NetTimerCallback* 函数都必须与不同的驱动程序分配和初始化的 timer 对象相关联。

调用 [**NdisSetTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject) 函数会导致与计时器对象关联的 *NetTimerCallback* 函数在指定间隔后或定期运行。

若要停止对 *NetTimerCallback* 函数的调用，请调用 [**NdisCancelTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject) 函数。 如果在调用**NdisCancelTimerObject**之前超时已过期，NDIS 仍可能会调用*NetTimerCallback* 。

如果 *NetTimerCallback* 函数与其他驱动程序函数共享资源，则驱动程序应使用自旋锁同步对这些资源的访问。

 

