---
title: TTD Range 对象
description: 本部分介绍与时间旅行调试关联的范围模型对象。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049dd6643565d218253a5c967819ee4f7e3e988b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568511"
---
# <a name="ttd-range-objects"></a>TTD Range 对象
## <a name="description"></a>描述
*TTD 范围*对象用于在跟踪中提供信息的时间范围。 这些通常用来描述的生存期[TTD 线程对象](time-travel-debugging-thread-objects.md)TTD 会话期间。

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| MinPosition | 一个[位置对象](time-travel-debugging-position-objects.md)，它描述与范围相关的最早位置。 |
| MaxPosition | 一个[位置对象](time-travel-debugging-position-objects.md)，它描述与范围相关的最新位置。 |


## <a name="example-usage"></a>示例用法

*挂起的信息*



## <a name="see-also"></a>请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


