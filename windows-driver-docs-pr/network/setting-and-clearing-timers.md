---
title: 设置和清除计时器
description: 设置和清除计时器
ms.assetid: 75f348f7-173f-4799-88aa-1ca50a6df023
keywords:
- timer 服务 WDK NDIS
- NDIS timer 服务 WDK
- 清除 NDIS 计时器
- 分配 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3e04575a38a808e08babfb7230e9bb445d8708e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841949"
---
# <a name="setting-and-clearing-timers"></a>设置和清除计时器





使用[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)函数分配和初始化计时器之后，NDIS 6.0 驱动程序将调用[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)函数来设置 timer 对象，使其在指定间隔后或定期触发。

**NdisSetTimerObject**的*DueTime*参数指定计时器触发之前经过的间隔，NDIS 调用关联的[**NetTimerCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)函数。 过期时间以系统时间单位（100毫微秒为间隔）表示。

如果**NdisSetTimerObject**的*MillisecondsPeriod*参数不为零，则计时器会定期触发， *MillisecondsPeriod*指定在每次定期计时器之间经过的周期性时间间隔（以毫秒为单位）激发并调用*NetTimerCallback*函数。

驱动程序可以调用[**NdisCancelTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)函数来取消与先前调用**NdisSetTimerObject**函数关联的计时器。 如果在调用**NdisCancelTimerObject**之前超时已过期，NDIS 仍可能会调用*NetTimerCallback* 。

 

 





