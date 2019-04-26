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
ms.openlocfilehash: a5109db1e49ffc0de0342fc5ef178780a8373815
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324937"
---
# <a name="initializing-ndis-timers"></a>初始化 NDIS 计时器





[ **NDIS\_计时器\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff567886)结构定义的一次性或定期计时器的特征。 任何 NDIS 驱动程序可以有多个计时器。 每个计时器对象都与其他相关联[ **NetTimerCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff568351)函数中指定**TimerFunction**成员。 NDIS 调用相关联*NetTimerCallback*函数在计时器过期时。

若要分配并初始化一个计时器，您的驱动程序应调用[ **NdisAllocateTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561618)函数，并提供驱动程序分配的 NDIS\_计时器\_特征结构。 驱动程序调用之前不会启动计时器[ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)函数。

若要释放的计时器对象，您的驱动程序应调用[ **NdisFreeTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff562605)函数。

 

 





