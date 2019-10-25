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
ms.openlocfilehash: 2a67f91fa6d548879d4dfc508f7d381151c6f50e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824437"
---
# <a name="initializing-ndis-timers"></a>初始化 NDIS 计时器





[**NDIS\_计时器\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_timer_characteristics)结构定义了一次拍摄或周期性计时器的特征。 任何 NDIS 驱动程序都可以有多个计时器。 每个计时器对象均与**TimerFunction**成员中指定的其他[**NetTimerCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)函数相关联。 当计时器过期时，NDIS 调用关联的*NetTimerCallback*函数。

若要分配和初始化计时器，驱动程序应调用[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)函数，并向驱动程序分配的 NDIS\_计时器\_特征结构。 在驱动程序调用[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)函数之前，计时器不会启动。

若要释放 timer 对象，驱动程序应调用[**NdisFreeTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreetimerobject)函数。

 

 





