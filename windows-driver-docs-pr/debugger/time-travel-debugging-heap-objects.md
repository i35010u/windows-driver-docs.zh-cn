---
title: TTD 堆对象
description: 本部分介绍与时间行程调试关联的堆模型对象。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21d1e2be8456ba705f68337196bc41b442a6692e
ms.sourcegitcommit: e94e072ef90fc1c4f343055098920463fbf5c630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227726"
---
# <a name="ttd-heap-objects"></a>TTD 堆对象
## <a name="description"></a>描述
*TTD 堆*对象用于给出有关在跟踪过程中发生的堆调用的信息。


## <a name="properties"></a>属性
每个堆对象将具有这些属性。

| 属性 | 描述 |
| --- | --- |
| 操作 | 描述发生的操作。 可能的值为：分配、ReAlloc、免费、创建、保护、锁定、解锁、销毁。 |
| 堆栈 | Win32 堆的句柄。 |

### <a name="conditional-properties"></a>条件属性
根据堆对象的不同，它可能具有以下某些属性。

| 属性 | 描述 |
| --- | --- |
| 地址 | 已分配的对象的地址。 |
| PreviousAddress | 在重新分配之前分配的对象的地址。 如果 Address 不同于 PreviousAddress，则重新分配导致内存移动。 |
| Size | 已分配对象的大小和/或请求的大小。 |
| BaseAddress | 堆中分配的对象的地址。  它可以表示将在重新分配对象之前释放（免费）或对象地址的地址（ReAlloc）。 |
| Flags | 这意味着依赖于 API。 |
| 结果 | 堆 API 调用的结果。 非零表示成功，零表示失败。 |
| ReserveSize | 要为堆预留的内存量。 |
| CommitSize | 堆的初始提交大小。 |
| MakeReadOnly | 非零值表示将堆设置为只读的请求;零值表示堆应为读写。 |

## <a name="children"></a>Children

| Object | 描述 |
| --- | --- |
| TimeStart | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述在分配开始时的位置。 |
| TimeEnd | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述分配末尾的位置。 |


## <a name="example-usage"></a>示例用法

使用此 dx 命令可以通过-g 选项显示网格中的堆内存。

```dbgcmd
0:0:000> dx -g @$cursession.TTD.Data.Heap()
=======================================================================================================================================================
=                          = Action     = Heap          = Address       = Size      = Flags  = (+) TimeStart = (+) TimeEnd = Result = PreviousAddress =
=======================================================================================================================================================
= [0x0] : [object Object]  - Alloc      - 0xaf0000      - 0xb0cfd0      - 0x4c      - 0x0    - FAB:17B1      - FAD:40      -        -                 =
= [0x1] : [object Object]  - Alloc      - 0xaf0000      - 0xb07210      - 0x34      - 0x8    - FB1:9         - FB3:74      -        -                 =
= [0x2] : [object Object]  - Alloc      - 0xaf0000      - 0xb256d8      - 0x3c      - 0x8    - E525:174      - E526:E1     -        -                 =
```


输出可以描述为 "已规范化数据"，因为有一组选择的 Api 表示堆操作。 从适当的参数中提取的数据以统一的方式呈现。

单击 TimeStart 或 TimeEnd 将在跟踪中导航到该点。  

单击特定条目旁边的 "参数" 字段，以显示可用的参数信息。

```dbgcmd
dx -r1 @$cursession.TTD.Data.Heap()[2].@"Parameters"
@$cursession.TTD.Data.Heap()[2].@"Parameters"                
    [0x0]            : 0x16c7d780000
    [0x1]            : 0x280000
    [0x2]            : 0x20
    [0x3]            : 0x0
```





## <a name="see-also"></a>请参阅

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)

---


