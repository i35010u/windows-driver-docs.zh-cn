---
title: TTD 内存对象
description: 本部分介绍与时间行程调试相关联的内存模型对象。
ms.date: 01/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b960859d1698518e451b555e0fce385af3bfac6
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916189"
---
# <a name="ttd-memory-objects"></a>TTD 内存对象

## <a name="description"></a>描述
*TTD 内存*是一种方法，该方法采用 BeginAddress、EndAddress 和 dataAccessMask 参数，并返回包含内存访问信息的内存对象的集合。

## <a name="parameters"></a>参数

| 属性 | 描述 |
| --- | --- |
| beginAddress | 以0x 开头的内存对象的开始地址。|
| endAddress| 以0x 开头的内存对象的结束地址。|
| dataAccessMask |双引号中包含的数据访问掩码。 这可以是 r 进行读取，w 用于写入，e 表示执行，c 表示更改。 |


## <a name="children"></a>Children

| 对象      | 描述 |
| ----------- | ----------- |
| EventType  |  事件的类型。 对于所有 TTD，这是 "MemoryAccess"。内存对象。 |
| ThreadId   |  发出请求的线程的操作系统线程 ID。 |
| UniqueThreadId |   跟踪内线程的唯一 ID。 可以在进程的生存期内重复使用常规线程 Id，但 UniqueThreadIds 不能。 |
| TimeStart | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述进行内存访问时的位置。 |
| TimeEnd | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述进行内存访问时的位置。 这将始终与 TTD 的 TimeStart 相同。内存对象。
| AccessType |  "访问类型"-"读取"、"写入" 或 "执行"。 |
| IP         |  进行内存访问的代码的指令指针。 |
| 地址    |  读取/写入/执行的地址，它将位于 [beginAddress，endAddress）范围内（从参数到）。内存（）。  请注意，间隔为半开。  也就是说，返回的任何事件都不会有地址匹配 endAddress，但也可能存在与 endAddress –1匹配的事件。|
| Size       |  读/写/执行的大小（以字节为单位）。 通常为8个字节或更少。 执行代码时，它是执行的指令中的字节数。 |
| Value   | 读取、写入或执行的值。 在执行时，它包含指令的代码字节。 请注意，指令字节按 MSB 顺序按反汇编程序列出，但将按 LSB 顺序存储在值中。 |


## <a name="remarks"></a>备注

允许在 TTD 中使用以下访问类型。内存查询：

-   r-读取
-   w-写入
-   读/写
-   电子执行
-   rwe-读取/写入/执行
-   ec-执行/change

请注意，这是一个执行计算的函数，因此需要一段时间才能运行。 


## <a name="example-usage"></a>示例用法

此示例显示了跟踪中的所有位置的网格显示，其中从0x00a4fca0 开始的四个字节的内存是读取访问。 单击任意条目，在每次出现内存访问时向下钻取。

```dbgcmd
dx -g @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")
```

![内存对象 dx 示例网格输出](images/ttd-time-travel-memory-object-dx-output.png) 

可以在网格显示的任何事件中单击 "TimeStart" 字段，以显示该事件的信息。 

```dbgcmd
0:000> dx -r1 @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart
@$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart                 : 5D:113 [Time Travel]
    Sequence         : 0x5d
    Steps            : 0x113
```

若要移动到跟踪中发生事件的位置，请单击 "时间段"。

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

在此示例中，列出了跟踪中从0x1bf7d0 开始的四个字节的内存，其中列出了读取/写入访问。 单击任意条目，在每次出现内存访问时向下钻取。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")
@$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")                
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]           
     ...
```
在此示例中，将列出跟踪中从 postions 开始的四个字节（从 "0x13a1710" 开始）的所有内存。 单击任意匹配项以查看有关每次出现内存访问的其他信息。  

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

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)

