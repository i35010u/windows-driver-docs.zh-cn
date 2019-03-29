---
title: TTD 异常对象
description: 本部分介绍与时间旅行调试相关联的异常模型对象。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1930ad42eda48937c3bf83393a7ff4b621d84246
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567643"
---
# <a name="ttd-exception-objects"></a>TTD 异常对象
## <a name="description"></a>描述
*TTD 异常*对象用于提供有关跟踪会话过程中发生的异常信息。


## <a name="properties"></a>属性

| 属性 | 描述 |
| --- | --- |
| 在任务栏的搜索框中键入 | 描述异常的类型。 可能的值为"软件"和"硬件"。 |
| ProgramCounter | 引发异常的指令。  |
| 代码 | 异常的代码。  |
| Flags | 异常的标志。 |
| RecordAddress | 您可以查找异常的记录的内存中的位置。  |

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| 位置 | 一个[位置对象](time-travel-debugging-position-objects.md)，描述发生异常的位置。 |

## <a name="example-usage"></a>示例用法

*挂起的信息*



## <a name="see-also"></a>请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


