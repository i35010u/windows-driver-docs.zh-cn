---
title: TTD 事件对象
description: 本部分介绍与时间旅行调试相关联的事件模型对象。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3511933227006dc5a5fe22b8c8da99a75dbfe887
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526747"
---
# <a name="ttd-event-objects"></a>TTD 事件对象
## <a name="description"></a>描述
*TTD 事件*对象用于提供有关时间旅行跟踪过程中发生的重要事件的信息。

## <a name="properties"></a>属性

| 属性 | 描述 |
| --- | --- |
| 在任务栏的搜索框中键入 | 描述发生的事件的类型。 可能的值为：ThreadCreated、 ThreadTerminated、 ModuleLoaded、 ModuleUnloaded、 异常 |

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| 位置 | 一个[位置对象](time-travel-debugging-position-objects.md)用于描述该事件发生的位置。 |
| 模块 * | 一个[模块对象](time-travel-debugging-module-objects.md)包含已加载或卸载的模块有关的信息。 |
| 线程 * | 一个[线程对象](time-travel-debugging-thread-objects.md)包含有关已创建或终止线程的信息。 |
| 异常 * | [异常对象](time-travel-debugging-exception-objects.md)包含有关异常已被命中的信息。 |

\* -这些子对象存在取决于事件的类型

## <a name="example-usage"></a>示例用法



```dbgcmd
0:000> dx -r2 @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
@$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)                
    [0x0]            : Exception of type CPlusPlus at PC: 0X777663B0
        Position         : 13B7:0 [Time Travel]
        Type             : CPlusPlus
        ProgramCounter   : 0x777663b0
        Code             : 0xe06d7363
        Flags            : 0x1
        RecordAddress    : 0x0
    [0x1]            : Exception of type Hardware at PC: 0XF1260D0
        Position         : BC0F:0 [Time Travel]
        Type             : Hardware
        ProgramCounter   : 0xf1260d0
        Code             : 0x80000003
        Flags            : 0x0
        RecordAddress    : 0x0
```


## <a name="see-also"></a>另请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


