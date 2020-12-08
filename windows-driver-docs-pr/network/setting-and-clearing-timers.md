---
title: 设置和清除计时器
description: 设置和清除计时器
keywords:
- timer 服务 WDK NDIS
- NDIS timer 服务 WDK
- 清除 NDIS 计时器
- 分配 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da9a34e70bcaf8cf38a33044a19f4e7990714f4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795907"
---
# <a name="setting-and-clearing-timers"></a>设置和清除计时器





使用 [**NdisAllocateTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject) 函数分配和初始化计时器之后，NDIS 6.0 驱动程序将调用 [**NdisSetTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject) 函数来设置 timer 对象，使其在指定间隔后或定期触发。

**NdisSetTimerObject** 的 *DueTime* 参数指定计时器触发之前经过的间隔，NDIS 调用关联的 [**NetTimerCallback**](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)函数。 过期时间以系统时间单位表示， (100 毫微秒间隔) 。

如果 **NdisSetTimerObject** 的 *MillisecondsPeriod* 参数不为零，则计时器会定期触发， *MillisecondsPeriod* 指定每次触发定期计时器和对 *NetTimerCallback* 函数的下一次调用之间的周期性时间间隔（以毫秒为单位）。

驱动程序可以调用 [**NdisCancelTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject) 函数来取消与先前调用 **NdisSetTimerObject** 函数关联的计时器。 如果在调用 **NdisCancelTimerObject** 之前超时已过期，NDIS 仍可能会调用 *NetTimerCallback* 。

 

