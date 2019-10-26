---
title: TTD 范围对象
description: 本部分介绍与时间行程调试关联的范围模型对象。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ba30a826e774255b8d94a7d3e194b55f1ead35d
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916180"
---
# <a name="ttd-range-objects"></a>TTD 范围对象

## <a name="description"></a>描述

*TTD 范围*对象用于为跟踪中的时间范围指定信息。 它们通常用于描述 TTD 会话期间[TTD 线程对象](time-travel-debugging-thread-objects.md)的生存期。

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| MinPosition | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述与范围相关的最早位置。 |
| MaxPosition | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述与范围相关的最晚位置。 |


## <a name="example-usage"></a>示例用法

*待处理信息*

## <a name="see-also"></a>另请参阅

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)

