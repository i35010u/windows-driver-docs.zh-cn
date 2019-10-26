---
title: TTD 异常对象
description: 本部分介绍与时间行程调试关联的异常模型对象。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7537ef96faf739c3ebf6d8e7b269e7602e3cc9a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916216"
---
# <a name="ttd-exception-objects"></a>TTD 异常对象

## <a name="description"></a>描述

*TTD Exception*对象用于给出有关在跟踪会话期间发生的异常的信息。


## <a name="properties"></a>“属性”

| 属性 | 描述 |
| --- | --- |
| 在任务栏的搜索框中键入 | 描述异常的类型。 可能的值为 "Software" 和 "硬件"。 |
| ProgramCounter | 引发了异常的指令。  |
| 代码 | 异常的代码。  |
| Flags | 异常标志。 |
| RecordAddress | 在内存中，可以找到异常记录。  |

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| 位置 | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述发生异常的位置。 |

## <a name="example-usage"></a>示例用法

*待处理信息*

## <a name="see-also"></a>另请参阅

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)
