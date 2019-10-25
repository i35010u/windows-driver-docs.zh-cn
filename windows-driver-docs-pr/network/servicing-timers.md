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
ms.openlocfilehash: 3276ec663f4a69761510e305df2578abac0c2cc1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841955"
---
# <a name="servicing-timers"></a>服务计时器





当 NDIS 6.0 计时器触发时，NDIS 将调用[**NetTimerCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)函数。 此函数的*FunctionContext*参数包含指向驱动程序提供的上下文区域的指针。 *FunctionContext*的默认值是在[**NDIS\_计时器\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_timer_characteristics)结构中指定的。 驱动程序将结构传递到[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)函数，以分配和初始化关联的计时器对象。

如果驱动程序在传递到[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)函数的*FunctionContext*参数中指定了非 NULL 值，则 NDIS 会将该值传递给*NetTimerCallback*函数的*FunctionContext*参数。 否则，NDIS 会将 NDIS\_计时器中指定的默认值传递\_特征结构。

任何 NDIS 驱动程序都可以有多个*NetTimerCallback*函数。 每个此类*NetTimerCallback*函数都必须与不同的驱动程序分配和初始化的 timer 对象相关联。

调用[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)函数会导致与计时器对象关联的*NetTimerCallback*函数在指定间隔后或定期运行。

若要停止对*NetTimerCallback*函数的调用，请调用[**NdisCancelTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)函数。 如果在调用**NdisCancelTimerObject**之前超时已过期，NDIS 仍可能会调用*NetTimerCallback* 。

如果*NetTimerCallback*函数与其他驱动程序函数共享资源，则驱动程序应使用自旋锁同步对这些资源的访问。

 

 





