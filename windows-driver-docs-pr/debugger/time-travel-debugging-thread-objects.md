---
title: TTD 线程对象
description: 本部分介绍与时间旅行调试相关联的线程模型对象。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5694c648acd00d3933db17cac8e46e661b8f0211
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541753"
---
# <a name="ttd-thread-objects"></a>TTD 线程对象
## <a name="description"></a>描述
*TTD 线程*对象用于提供有关线程和其生存期期间移动跟踪的信息。

## <a name="properties"></a>属性

| 属性 | 描述 |
| --- | --- |
| UniqueId | 跟踪跨线程的唯一 ID。 |
| ID | 线程的该 TID。 |


## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| LifeTime | 一个[TTD 范围对象](time-travel-debugging-range-objects.md)描述的线程的生存期。 |
| ActiveTime | 一个[TTD 范围对象](time-travel-debugging-range-objects.md)用于描述该线程处于活动状态的时间。 |


## <a name="example-usage"></a>示例用法

使用此 dx 命令数组中显示的所有线程。

```dbgcmd
0:0:000> dx -g @$curprocess.TTD.Threads
=================================================================================================================
=                             = (+) UniqueId = (+) Id    = (+) Lifetime                 = (+) ActiveTime        =
=================================================================================================================
= [0x0] : UID: 2, TID: 0x2428 - 0x2          - 0x2428    - [0:0, 6F0C4:0]               - [50C63:0, 6F0C4:0]    =
= [0x1] : UID: 3, TID: 0x3520 - 0x3          - 0x3520    - [0:0, FFFFFFFFFFFFFFFE:0]    - [5115A:0, 56B07:0]    =
= [0x2] : UID: 4, TID: 0x18E8 - 0x4          - 0x18e8    - [0:0, FFFFFFFFFFFFFFFE:0]    - [52F65:0, 56B1E:0]    =
= [0x3] : UID: 5, TID: 0x5690 - 0x5          - 0x5690    - [0:0, FFFFFFFFFFFFFFFE:0]    - [5300D:0, 5D4FA:0]    =
= [0x4] : UID: 6, TID: 0x46FC - 0x6          - 0x46fc    - [0:0, FFFFFFFFFFFFFFFE:0]    - [53782:0, 5433B:0]    =
= [0x5] : UID: 7, TID: 0x58D0 - 0x7          - 0x58d0    - [0:0, FFFFFFFFFFFFFFFE:0]    - [542FE:0, 543B9:0]    =
= [0x6] : UID: 8, TID: 0x950  - 0x8          - 0x950     - [0:0, FFFFFFFFFFFFFFFE:0]    - [543C4:0, 544B8:0]    =
= [0x7] : UID: 9, TID: 0x4514 - 0x9          - 0x4514    - [0:0, 6D61B:0]               - [5DBBD:0, 6D61B:0]    =
=================================================================================================================
```

使用此 dx 命令数组中显示的第一个线程有关的信息。

```dbgcmd
0:0:000 dx -r2 @$curprocess.TTD.Threads[0]
@$curprocess.TTD.Threads[0]                 : UID: 2, TID: 0x2428
    UniqueId         : 0x2
    Id               : 0x2428
    Lifetime         : [0:0, 6F0C4:0]
        MinPosition      : Min Position [Time Travel]
        MaxPosition      : 6F0C4:0 [Time Travel]
    ActiveTime       : [50C63:0, 6F0C4:0]
        MinPosition      : 50C63:0 [Time Travel]
        MaxPosition      : 6F0C4:0 [Time Travel]
```

当线程处于活动状态时，[时程] 链接将提供指向 SeekTo() 在跟踪中的特定位置。 

```dbgcmd
0:0:000> dx @$curprocess.TTD.Threads[0].@"ActiveTime".@"MinPosition".SeekTo()
Setting position: 50C63:0
@$curprocess.TTD.Threads[0].@"ActiveTime".@"MinPosition".SeekTo()
(40b4.2428): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 50C63:0
ntdll!NtTestAlert+0x14:
00007ffb`e3e289d4 c3              ret
```


## <a name="see-also"></a>另请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


