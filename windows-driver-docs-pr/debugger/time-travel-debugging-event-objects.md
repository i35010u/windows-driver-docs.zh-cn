---
title: TTD 事件对象
description: 本部分介绍与时间行程调试关联的事件模型对象。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99c5a84dc57edad2eebac21fb6185fafc5595cb2
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916217"
---
# <a name="ttd-event-objects"></a>TTD 事件对象

## <a name="description"></a>描述
*TTD 事件*对象用于给出有关在时间行程跟踪期间发生的重要事件的信息。

## <a name="properties"></a>“属性”

| 属性 | 描述 |
| --- | --- |
| 在任务栏的搜索框中键入 | 描述发生的事件的类型。 可能的值包括： ThreadCreated、ThreadTerminated、ModuleLoaded、ModuleUnloaded、Exception |

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| 位置 | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述事件发生的位置。 |
| 模块 | 一个[module 对象](time-travel-debugging-module-objects.md)，其中包含有关已加载或卸载的模块的信息。 |
| Thread | 一个[线程对象](time-travel-debugging-thread-objects.md)，其中包含有关已创建或终止的线程的信息。 |
| 异常 | 一个[异常对象](time-travel-debugging-exception-objects.md)，其中包含有关所命中的异常的信息。 |

\*-这些子对象是否存在取决于事件的类型

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

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)
