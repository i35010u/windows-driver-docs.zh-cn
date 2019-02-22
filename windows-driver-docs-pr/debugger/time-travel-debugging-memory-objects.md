---
title: TTD 内存对象
description: 本部分介绍与时间旅行调试相关联的内存模型对象。
ms.date: 01/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: aaa9dc8d392fa4f14ef5df663bd1a657c2965502
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545940"
---
# <a name="ttd-memory-objects"></a>TTD 内存对象
## <a name="description"></a>描述
*TTD 内存*是一种方法接受 beginAddress、 endAddress 和 dataAccessMask 参数并返回包含内存访问信息的内存对象的集合。

## <a name="parameters"></a>参数

| 属性 | 描述 |
| --- | --- |
| beginAddress | 内存对象以 0x 开头的起始地址。|
| endAddress| 内存对象以 0x 开头的结束地址。|
| dataAccessMask |包含在双引号内数据访问掩码。 这可以在读取、 写入、 e 表示 execute 和更改 c w r。 |


## <a name="children"></a>Children

| 对象      | 描述 |
| ----------- | ----------- |
| EventType  |  事件的类型。 这是为所有 TTD"MemoryAccess"。内存对象。 |
| ThreadId   |  发出请求的线程的操作系统线程 ID。 |
| UniqueThreadId |   跟踪跨线程的唯一 ID。 常规线程 Id 可获取进程的生存期内重复使用，但 UniqueThreadIds 不能。 |
| TimeStart | 一个[位置对象](time-travel-debugging-position-objects.md)的描述时进行内存访问的位置。 |
| TimeEnd | 一个[位置对象](time-travel-debugging-position-objects.md)的描述时进行内存访问的位置。 此属性始终为 TTD TimeStart 相同。内存对象。
| AccessType |  访问类型的读取、 写入或执行。 |
| IP         |  所做的内存访问的代码指令指针。 |
| 地址    |  已读取 / 写入 / 执行的地址并将处于的范围 [beginAddress, endAddress) 从的参数。Memory()。  请注意，该间隔是半开。  也就是说，没有任何返回的事件将具有匹配 endAddress，但可以匹配 endAddress – 1 的事件。|
| 尺寸       |  读取/写入/执行以字节为单位的大小。 这通常是 8 个字节或更少。 发生时执行代码，它是已执行的指令中的字节数。 |
| 值   | 读取、 写入或执行的值。 如果执行，它包含指令的代码字节。 请注意指令字节拆装器 MSB 顺序列出，但将存储在 LSB 顺序的值。 |


## <a name="remarks"></a>备注

TTD 中允许使用以下访问权限类型。内存查询：

-   r-读取
-   w-写入
-   rw-读取/写入
-   e-执行
-   rwe-读取 / 写入/执行
-   ec-执行/更改

请注意，这是执行计算，因此需要一段时间才能运行的函数。 


## <a name="example-usage"></a>示例用法

此示例中显示的所有四个字节的内存从 0x00a4fca0 处开始，已读取访问权限的位置在跟踪中的网格显示出错。 单击向下钻取每个发生内存访问的任何条目。

```dbgcmd
dx -g @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")
```

![内存对象 dx 示例网格输出](images/ttd-time-travel-memory-object-dx-output.png) 

您可以单击的 TimeStart 字段中的任何事件网格显示，以显示该事件的信息中。 

```dbgcmd
0:000> dx -r1 @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart
@$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart                 : 5D:113 [Time Travel]
    Sequence         : 0x5d
    Steps            : 0x113
```

若要将移动到发生事件的跟踪中的位置，单击 [时程]。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart.SeekTo()
@$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart.SeekTo()
(27b8.3168): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 5D:113

eax=0000004c ebx=00dd0000 ecx=00a4f89c edx=00a4f85c esi=00a4f89c edi=00b61046
eip=690795e5 esp=00a4f808 ebp=00a4f818 iopl=0         nv up ei pl nz na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
690795e5 ffb604040000    push    dword ptr [esi+404h] ds:002b:00a4fca0=00000000
```

在此示例中，会列出所有在跟踪中的四个字节的内存开始 0x1bf7d0 处于读/写访问的位置。 单击向下钻取每个发生内存访问的任何条目。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")
@$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")                
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]           
     ...
```
在此示例中会列出所有 postions 其中四个字节的 0x13a1710 处开始的内存已访问/执行更改跟踪中。 单击任何实例以向下钻取每个匹配项上的内存访问的其他信息。  

```dbgcmd
0:000> dx -r1 @$cursession.TTD.Memory(0x13a1710,0x13a1714, "ec")[0]
@$cursession.TTD.Memory(0x13a1710,0x13a1714, "ec")[0]                
    EventType        : MemoryAccess
    ThreadId         : 0x1278
    UniqueThreadId   : 0x2
    TimeStart        : 5B:4D [Time Travel]
    TimeEnd          : 5B:4D [Time Travel]
    AccessType       : Execute
    IP               : 0x13a1710
    Address          : 0x13a1710
    Size             : 0x1
    Value            : 0x55
```



## <a name="see-also"></a>另请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


