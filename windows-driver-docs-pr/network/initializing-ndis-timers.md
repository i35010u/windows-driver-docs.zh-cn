---
title: 初始化 NDIS 计时器
description: 初始化 NDIS 计时器
ms.assetid: 2f304f5c-fa70-441e-853e-a48ad70d61a0
keywords:
- timer 服务 WDK NDIS
- NDIS timer 服务 WDK
- 初始化 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b84f09e22f947c795ac3ac4780261def14d423eb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206749"
---
# <a name="initializing-ndis-timers"></a>初始化 NDIS 计时器





[**NDIS \_ 计时器 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_timer_characteristics)结构定义了一次拍摄或周期性计时器的特征。 任何 NDIS 驱动程序都可以有多个计时器。 每个计时器对象均与**TimerFunction**成员中指定的其他[**NetTimerCallback**](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)函数相关联。 当计时器过期时，NDIS 调用关联的 *NetTimerCallback* 函数。

若要分配和初始化计时器，驱动程序应调用 [**NdisAllocateTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject) 函数并提供驱动程序分配的 NDIS \_ 计时器 \_ 特征结构。 在驱动程序调用 [**NdisSetTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject) 函数之前，计时器不会启动。

若要释放 timer 对象，驱动程序应调用 [**NdisFreeTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreetimerobject) 函数。

 

