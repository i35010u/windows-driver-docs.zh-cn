---
title: TTD 调用对象
description: 本部分介绍与时间行程调试关联的模型对象。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3576f064e7baddd963cedb6593c7b4ac96b4e4
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916219"
---
# <a name="ttd-calls-objects"></a>TTD 调用对象

## <a name="description"></a>描述
*TTD 调用*对象用于对在跟踪过程中发生的函数调用进行相关的信息。

## <a name="parameters"></a>参数

| 属性 | 描述 |
| --- | --- |
| 才能!SymbolName | 一个或多个包含在双引号中，用逗号分隔。 例如 dx @ $cursession。TTD.调用（"module！ symbol1"，"module！ symbol2"，...） |

## <a name="properties"></a>“属性”

| 属性 | 描述 |
| --- | --- |
| EventType  |  事件的类型。 这是所有 TTD 调用对象的 "调用"。 |
| ThreadId   |  发出请求的线程的操作系统线程 ID。 |
| UniqueThreadId |   跟踪内线程的唯一 ID。 可以在进程的生存期内重复使用常规线程 Id，但 UniqueThreadIds 不能。 |
| 函数 | 函数的符号名称。 |
| FunctionAddress | 内存中的函数地址。 |
| ReturnValue | 函数的返回值。 如果函数具有 void 类型，则此属性将不存在。 |

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| Parameters [] | 包含传递给函数的参数的数组。 元素数目根据函数的类型签名而变化。 |
| TimeStart | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述调用开始时的位置。 |
| TimeEnd | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述调用结束时的位置。 |

## <a name="remarks"></a>备注
行程调试使用 Pdb 中提供的符号信息来确定函数的参数数目及其类型、返回值类型和调用约定。 如果符号信息不可用或符号被限制为公共符号信息，则仍可执行查询。 在这种情况下，旅行查询引擎将做出一些假设：
* 函数包含 4 64 位无符号整数参数
* 返回值为64位无符号整数
* 函数名称设置为固定字符串： "UnknownOrMissingSymbols"

这些假设允许在没有足够的符号信息的情况中进行查询。 但是，为了获得最佳效果，请尽可能使用完整的 PDB 符号。

请注意，调用函数进行计算，并根据跟踪的大小，可能需要一段时间才能运行。 在计算和监视 CPU 使用情况下，CPU 使用率将在任务管理器中显示，并提供计算正在进行的指示。  查询结果将缓存在内存中，因此，对之前查询的调用进行的后续查询的速度要快得多。

## <a name="example-usage"></a>示例用法

此示例显示了 ucrtbase.dll！ initterm 的调用对象。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("ucrtbase!initterm")
@$cursession.TTD.Calls("ucrtbase!initterm")
    [0x0]
        EventType        : Call
        ThreadId         : 0x2074
        UniqueThreadId   : 0x2
        TimeStart        : 1E:5D0
        TimeEnd          : 2D:E
        Function         : ucrtbase!_initterm
        FunctionAddress  : 0x7ffb345825d0
        ReturnAddress    : 0x7ff6a521677e
        Parameters
```

## <a name="see-also"></a>另请参阅

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)
