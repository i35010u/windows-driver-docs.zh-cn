---
title: TTD 堆对象
description: 本部分介绍与时间旅行调试关联的堆模型对象。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29bbd1e05ed966095eebff5655db0e72c885592f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389099"
---
# <a name="ttd-heap-objects"></a>TTD 堆对象
## <a name="description"></a>描述
*TTD 堆*对象用于提供有关堆调用发生在过去的跟踪的信息。


## <a name="properties"></a>属性
每个堆对象将具有这些属性。

| 属性 | 描述 |
| --- | --- |
| 操作 | 描述发生的操作。 可能的值为：分配、 ReAlloc、 Free，创建、 保护、 锁定、 解锁、 销毁。 |
| 堆 | Win32 堆的句柄。 |

### <a name="conditional-properties"></a>条件属性
根据堆对象，它可能具有的某些属性下面。

| 属性 | 描述 |
| --- | --- |
| 地址 | 已分配的对象的地址。 |
| PreviousAddress | 之前已重新分配已分配的对象的地址。 如果地址不是与 PreviousAddress 相同重新分配操作将导致要移动的内存。 |
| 大小 | 大小和/或请求的已分配的对象的大小。 |
| BaseAddress | 在堆中分配的对象的地址。  它可以表示该地址将释放 (Free) 或在其之前的对象的地址重新分配 (ReAlloc。) |
| Flags | 含义取决于该 API。 |
| 结果 | 调用堆 API 的结果。 非零表示成功，零表示失败。 |
| ReserveSize | 要保留为堆的内存量。 |
| CommitSize | 堆的初始提交的大小。 |
| MakeReadOnly | 一个非零值指示只读的; 请在堆的请求零值表示堆应为读写。 |

## <a name="children"></a>Children

| Object | 描述 |
| --- | --- |
| TimeStart | 一个[位置对象](time-travel-debugging-position-objects.md)描述分配的开始处的位置。 |
| TimeEnd | 一个[位置对象](time-travel-debugging-position-objects.md)，它描述在分配末尾的位置。 |


## <a name="example-usage"></a>示例用法

使用此 dx 命令使用-g 选项网格中显示的堆内存。

```dbgcmd
0:0:000> dx -g @$cursession.TTD.Data.Heap()
==================================================================================================================================
=           = (+) Function               = (+) FunctionAddress = (+) ReturnValue  = (+) Parameters = (+) TimeStart = (+) TimeEnd =
==================================================================================================================================
= [0x0]     - UnknownOrMissingSymbols    - 0x7ffbe3daae00      - 0x16c7d7b4050    - {...}          - 50C74:8E      - 50C76:3B    =
= [0x1]     - UnknownOrMissingSymbols    - 0x7ffbe3db0dd0      - 0x1              - {...}          - 50C76:1E9     - 50C78:1D    =
= [0x2]     - UnknownOrMissingSymbols    - 0x7ffbe3daae00      - 0x16c7d7be400    - {...}          - 51C95:21F3    - 51CA6:81    =
```


输出可以被描述为"规范化数据"，因为所选的一组 Api，表示堆操作。 从相应的参数中提取数据以统一的方式显示。

单击 TimeStart 或时间结束会将您导航到该点则在跟踪中。  

单击参数字段旁边的特定条目，以显示可用的参数信息。

```dbgcmd
dx -r1 @$cursession.TTD.Data.Heap()[2].@"Parameters"
@$cursession.TTD.Data.Heap()[2].@"Parameters"                
    [0x0]            : 0x16c7d780000
    [0x1]            : 0x280000
    [0x2]            : 0x20
    [0x3]            : 0x0
```





## <a name="see-also"></a>请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


