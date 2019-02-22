---
title: IEEE 802.1p 优先级级别
description: IEEE 802.1p 优先级级别
ms.assetid: C7EB3D85-544E-4898-A456-843621F6488D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c91917211c16566728241d5999597a03d2e129
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543272"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p 优先级级别


IEEE 802.1p 由 IEEE 802.1 任务指定的组，以满足服务质量 (QoS) 的通信优先级。 802.1p 不是单独的 IEEE 802.1 标准，但在 IEEE 802.1Q 的附录 G 中定义的标准 2005年。

IEEE 802.1p 定义一个名为 IEEE 802.1Q 中优先级代码点 (PCP) 的 3 位字段标记。 NDIS 数据包的 802.1p PCP 值由指定**UserPriority**的成员[ **NDIS\_NET\_缓冲区\_列表\_8021Q\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566565)结构，它是与数据包的关联[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

PCP 值定义 8 的优先级别，7，最高优先级和 1 的最低优先级。 默认值为 0 的优先级别。 每个优先级别定义*的服务类*标识传输数据包的单独通信类。

 

 





