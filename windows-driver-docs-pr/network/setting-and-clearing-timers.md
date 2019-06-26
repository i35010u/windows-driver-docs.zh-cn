---
title: 设置和清除计时器
description: 设置和清除计时器
ms.assetid: 75f348f7-173f-4799-88aa-1ca50a6df023
keywords:
- 计时器服务 WDK NDIS
- NDIS 计时器服务 WDK
- 清除 NDIS 计时器
- 分配 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 314383af86e25d56000ebf75e3bd06ee53c75255
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373867"
---
# <a name="setting-and-clearing-timers"></a>设置和清除计时器





分配并初始化与计时器后[ **NdisAllocateTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatetimerobject)函数，NDIS 6.0 驱动程序调用[ **NdisSetTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)函数可设置指定的时间间隔之后或定期触发的计时器对象。

*DueTime*的参数**NdisSetTimerObject**指定计时器将激发并 NDIS 调用关联之前等待的时间间隔[ **NetTimerCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_timer_function)函数。 过期时间被以系统时间单位 （100 纳秒间隔）。

如果*MillisecondsPeriod*的参数**NdisSetTimerObject**不为零，计时器将触发定期并*MillisecondsPeriod*指定的定期时间每次启动定期计时器和的后续调用之间的间隔时间间隔，以毫秒为单位， *NetTimerCallback*函数。

您的驱动程序可以调用[ **NdisCancelTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)函数取消与以前调用相关联的计时器**NdisSetTimerObject**函数。 可能仍需调用 NDIS *NetTimerCallback*如果在超时已过期之前调用**NdisCancelTimerObject**。

 

 





