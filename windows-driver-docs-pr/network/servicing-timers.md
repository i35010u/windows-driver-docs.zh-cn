---
title: 服务计时器
description: 服务计时器
ms.assetid: 6a80a55b-4c7e-4a48-8903-0a1fb28af153
keywords:
- 计时器服务 WDK NDIS
- NDIS 计时器服务 WDK
- 正在取消 NDIS 计时器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec4998691069a9d23c8676d313ecf74fde2f185a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346749"
---
# <a name="servicing-timers"></a>服务计时器





NDIS 调用[ **NetTimerCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff568351) NDIS 6.0 计时器将激发时的功能。 *FunctionContext*此函数的参数包含驱动程序提供的上下文区域的指针。 默认值为*FunctionContext*中指定[ **NDIS\_计时器\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff567886)结构。 该驱动程序传递的结构[ **NdisAllocateTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561618)函数以分配并初始化关联的计时器对象。

如果该驱动程序中指定了非 NULL 值*FunctionContext*参数传递给[ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)函数，NDIS 将该值传递到*FunctionContext*的参数*NetTimerCallback*函数。 否则，NDIS 传递 NDIS 中指定的默认值\_计时器\_特征结构。

任何 NDIS 驱动程序可以有多个*NetTimerCallback*函数。 每个此类*NetTimerCallback*函数必须与不同的驱动程序分配并初始化计时器对象相关联。

调用[ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)函数的原因*NetTimerCallback*与要在指定时间间隔之后运行的计时器对象相关联的函数或定期。

若要停止对调用*NetTimerCallback*函数中，调用[ **NdisCancelTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561624)函数。 可能仍需调用 NDIS *NetTimerCallback*如果在超时已过期之前调用**NdisCancelTimerObject**。

如果*NetTimerCallback*函数与其他驱动程序函数共享资源、 驱动程序应与旋转锁来同步对这些资源的访问。

 

 





