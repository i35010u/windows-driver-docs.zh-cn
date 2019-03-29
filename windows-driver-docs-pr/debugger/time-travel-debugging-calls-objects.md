---
title: TTD 调用对象
description: 本部分中描述的调用模型与时间旅行调试相关联的对象。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9300b2b472ac0a354f9e0a08f1c1f7c5d914a8de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562801"
---
# <a name="ttd-calls-objects"></a>TTD 调用对象
## <a name="description"></a>描述
*TTD 调用*对象用于提供有关发生在过去的跟踪的函数调用的信息。

## <a name="parameters"></a>Parameters

| 属性 | 描述 |
| --- | --- |
| Function!SymbolName | 一个或多个包含在双引号内，用逗号隔开。 For example dx @$cursession.TTD.Calls("module!symbol1", "module!symbol2", ...) |

## <a name="properties"></a>属性

| 属性 | 描述 |
| --- | --- |
| EventType  |  事件的类型。 这是用于所有 TTD 调用对象的"Call"。 |
| ThreadId   |  发出请求的线程的操作系统线程 ID。 |
| UniqueThreadId |   跟踪跨线程的唯一 ID。 常规线程 Id 可获取进程的生存期内重复使用，但 UniqueThreadIds 不能。 |
| 函数 | 函数的符号名称。 |
| FunctionAddress | 在内存中的函数的地址。 |
| ReturnValue | 该函数返回值。 如果函数具有 void 类型，此属性将不会显示。 |

## <a name="children"></a>Children

| 对象 | 描述 |
| --- | --- |
| Parameters[] | 包含参数的数组传递给函数。 根据函数的类型签名的元素数而异。 |
| TimeStart | 一个[位置对象](time-travel-debugging-position-objects.md)，它描述调用的开始处的位置。 |
| TimeEnd | 一个[位置对象](time-travel-debugging-position-objects.md)，它描述调用末尾处的位置。 |

## <a name="remarks"></a>备注
时间旅行调试使用 Pdb 中提供的符号信息来确定的函数和它们的类型、 返回值类型和调用约定的参数数目。 如果符号信息不可用或符号已被限制为公共符号信息，则仍可以执行的查询。 时间旅行查询引擎将在此方案中做出一些假设：
* 有四个 64 位无符号的整数参数对函数
* 返回值是 64 位无符号的整数
* 函数名称设置为固定字符串：“UnknownOrMissingSymbols”

这些假设允许在没有足够的符号信息中进行的查询。 但是，为了获得最佳结果使用完整的 PDB 符号在可能的情况。

请注意，调用函数执行计算，具体取决于所跟踪的大小，可能需要一段时间才能运行。 CPU 使用率在计算期间会剧增，并观看任务管理器中的 CPU 使用率提供指示，则会进行计算时的进展情况。  查询结果会缓存在内存中，因此对以前查询调用后续查询时速度明显加快。



## <a name="example-usage"></a>示例用法

此示例演示 ucrtbase 调用对象 ！ initterm。

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




## <a name="see-also"></a>请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


