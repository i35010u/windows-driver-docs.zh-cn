---
title: TTD 线程对象
description: 本部分介绍与时间行程调试相关联的线程模型对象。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0d38085e78f03dc80ee63facaf3a16dab87c6b4e
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916138"
---
# <a name="ttd-thread-objects"></a>TTD 线程对象

## <a name="description"></a>描述

*TTD 线程*对象用于在时间段跟踪期间为线程及其生存期生成信息。

## <a name="properties"></a>“属性”

| 属性 | 描述 |
| --- | --- |
| UniqueId | 跟踪内线程的唯一 ID。 |
| ID | 线程的 TID。 |


## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| 生存期 | 描述线程生存期的[TTD 范围对象](time-travel-debugging-range-objects.md)。 |
| ActiveTime | 描述线程处于活动状态的时间的[TTD 范围对象](time-travel-debugging-range-objects.md)。 |


## <a name="example-usage"></a>示例用法

使用此 dx 命令可显示数组中的所有线程。

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

使用此 dx 命令显示有关数组中第一个线程的信息。

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

当线程处于活动状态时，[Time 旅行] 链接提供指向跟踪中特定位置的 SeekTo （）的链接。 

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

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)
