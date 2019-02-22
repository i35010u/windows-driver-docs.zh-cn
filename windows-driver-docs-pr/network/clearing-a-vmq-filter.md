---
title: 正在清除 VMQ 筛选器
description: 正在清除 VMQ 筛选器
ms.assetid: 34efeb28-dcd6-4a8b-89d2-6065830e03ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2174e0490c1f94040acbc3289141c6ed67b978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541717"
---
# <a name="clearing-a-vmq-filter"></a>正在清除 VMQ 筛选器





要释放接收队列中的筛选器，基础驱动程序将发出[OID\_接收\_筛选器\_清除\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569785)集 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_清除\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567166)结构。

从早期协议驱动程序获取筛选器标识符[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)方法 OID 请求。 有关设置筛选器的详细信息，请参阅[VMQ 筛选器设置](setting-a-vmq-filter.md)。

协议驱动程序必须清除它在释放队列前在队列设置的所有筛选器。 协议驱动程序还必须清除它的默认队列，然后设置关闭其绑定到的网络适配器的所有筛选器。

微型端口驱动程序必须指示非默认队列上的数据包，如果它已完成 OID\_接收\_筛选器\_清除\_对清除队列上的最后一个筛选器或如果它已完成筛选器OID请求[OID\_接收\_筛选器\_免费\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569789)OID 请求以释放队列。

 

 





