---
title: 初始化 NDIS 计时器
description: 初始化 NDIS 计时器
ms.assetid: 2f304f5c-fa70-441e-853e-a48ad70d61a0
keywords:
- 计时器服务 WDK NDIS
- NDIS 计时器服务 WDK
- 初始化 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9246a24925be737321867b1456437e5aa1b06ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381268"
---
# <a name="initializing-ndis-timers"></a>初始化 NDIS 计时器





[ **NDIS\_计时器\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_timer_characteristics)结构定义的一次性或定期计时器的特征。 任何 NDIS 驱动程序可以有多个计时器。 每个计时器对象都与其他相关联[ **NetTimerCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_timer_function)函数中指定**TimerFunction**成员。 NDIS 调用相关联*NetTimerCallback*函数在计时器过期时。

若要分配并初始化一个计时器，您的驱动程序应调用[ **NdisAllocateTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatetimerobject)函数，并提供驱动程序分配的 NDIS\_计时器\_特征结构。 驱动程序调用之前不会启动计时器[ **NdisSetTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)函数。

若要释放的计时器对象，您的驱动程序应调用[ **NdisFreeTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreetimerobject)函数。

 

 





