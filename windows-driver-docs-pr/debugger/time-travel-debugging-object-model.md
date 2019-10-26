---
title: 时光穿越调试 - 时光穿越调试对象简介
description: 本部分介绍如何使用数据模型查询时间行程跟踪。
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 80012c5dc98ad8c049ef18fb53158857ff9c4b2a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916186"
---
# <a name="introduction-to-time-travel-debugging-objects"></a>行程调试对象简介

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

本部分介绍如何使用数据模型查询时间行程跟踪。 这可以是一个功能强大的工具，可用于回答有关在时间行程跟踪中捕获的代码等问题。
* 跟踪中有哪些例外？
* 跟踪中的哪个时间点执行特定的代码模块加载？
* 在跟踪中创建/终止线程的时间
* 跟踪中运行时间最长的线程是多少？

存在将数据添加到*会话*并*处理*数据模型对象的 TTD 扩展。 可以通过[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)命令、WinDbg Preview 的模型窗口、JavaScript 和C++来访问 TTD 数据模型对象。 调试时间行程跟踪时，会自动加载 TTD 扩展。

## <a name="process-objects"></a>处理对象

可以在任何*进程*对象的*TTD*命名空间中找到添加到*进程*对象的主对象。 例如，`@$curprocess.TTD`。

```dbgcmd
:000> dx @$curprocess.TTD
@$curprocess.TTD                
    Threads         
    Events          
    Lifetime         : [26:0, 464232:0]
    SetPosition      [Sets the debugger to point to the given position on this process.]
```

有关使用 LINQ 查询和调试器对象的常规信息，请参阅[将 Linq 与调试器对象配合使用](using-linq-with-the-debugger-objects.md)。

### <a name="properties"></a>“属性”

| 对象 | 描述 |
| --- | --- |
| 生存期 | 描述整个跟踪的生存期的[TTD 范围对象](time-travel-debugging-range-objects.md)。 |
| 线程 | 包含[TTD 线程对象](time-travel-debugging-thread-objects.md)的集合，每个线程在跟踪的整个生存期内都一个。 |
| 事件 | 包含[TTD 事件对象](time-travel-debugging-event-objects.md)的集合，其中每个事件都对应于跟踪中的每个事件。 |

### <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| SetPosition （） | 采用0到100之间的整数或以 N：N 形式表示的字符串作为输入，并将跟踪跳转到该位置。 有关详细信息，请参阅[！ tt](time-travel-debugging-extension-tt.md) 。|

## <a name="session-objects"></a>会话对象
可在任何*会话*对象的*TTD*命名空间中找到添加到*会话*对象的主对象。 例如，`@$cursession.TTD`。

```dbgcmd
0:000> dx @$cursession.TTD
@$cursession.TTD                 : [object Object]
    Calls            [Returns call information from the trace for the specified set of methods: TTD.Calls("module!method1", "module!method2", ...) For example: dx @$cursession.TTD.Calls("user32!SendMessageA")]
    Memory           [Returns memory access information for specified address range: TTD.Memory(startAddress, endAddress [, "rwec"])]
    DefaultParameterCount : 0x4
    AsyncQueryEnabled : false
    Resources       
    Data             : Normalized data sources based on the contents of the time travel trace
    Utility          : Methods that can be useful when analyzing time travel traces
```


> [!NOTE]
> TTDAnalyze 添加了一些对象和方法，这些对象和方法用于扩展的内部函数。 并不是所有的命名空间都有记录，当前的命名空间将随着时间的推移而演化。
>

### <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| 数据集（） | 在跟踪过程中分配的[堆对象](time-travel-debugging-heap-objects.md)的集合。 请注意，这是一个执行计算的函数，因此需要一段时间才能运行。|
| 调用（） | 返回一个集合，该集合调用与输入字符串匹配的[对象](time-travel-debugging-calls-objects.md)。 输入字符串可以包含通配符。 请注意，这是一个执行计算的函数，因此需要一段时间才能运行。  |
| 内存（） | 此方法采用 beginAddress、endAddress 和 dataAccessMask 参数，并返回[内存对象](time-travel-debugging-memory-objects.md)的集合。 请注意，这是一个执行计算的函数，因此需要一段时间才能运行。  |


## <a name="sorting-query-output"></a>排序查询输出

使用 OrderBy （）方法对一个或多个列从查询返回的行进行排序。 此示例按 TimeStart 按升序排序。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").OrderBy(c => c.TimeStart)
@$cursession.TTD.Calls("kernelbase!GetLastError").OrderBy(c => c.TimeStart)                
    [0xb]           
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : 39:2DC [Time Travel]
        TimeEnd          : 39:2DF [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x7593d24c
        ReturnValue      : 0x0
        Parameters      
    [0xe]           
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : AF:36 [Time Travel]
        TimeEnd          : AF:39 [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x4723ef
        ReturnValue      : 0x0
        Parameters  
```

若要显示数据模型对象的其他深度，请使用-r2 递归级别选项。 有关 dx 命令选项的详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

此示例按 TimeStart 按降序排序。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").OrderByDescending(c => c.TimeStart)
@$cursession.TTD.Calls("kernelbase!GetLastError").OrderByDescending(c => c.TimeStart)                
    [0x1896]        
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : 464224:34 [Time Travel]
        TimeEnd          : 464224:37 [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x7594781c
        ReturnValue      : 0x0
        Parameters      
    [0x18a0]        
        EventType        : Call
        ThreadId         : 0x3a10
        UniqueThreadId   : 0x2
        TimeStart        : 464223:21 [Time Travel]
        TimeEnd          : 464223:24 [Time Travel]
        Function         : UnknownOrMissingSymbols
        FunctionAddress  : 0x7561ccc0
        ReturnAddress    : 0x7594781c
        ReturnValue      : 0x0
        Parameters    
```

## <a name="specifying-elements-in-a-query"></a>指定查询中的元素

若要选择特定元素，可以在查询中追加各种限定符。 例如，查询将显示第一次调用，其中包含 "kernelbase！GetLastError "。

```dbgcmd
0:000> dx @$cursession.TTD.Calls("kernelbase!GetLastError").First()
@$cursession.TTD.Calls("kernelbase!GetLastError").First()                
    EventType        : Call
    ThreadId         : 0x3a10
    UniqueThreadId   : 0x2
    TimeStart        : 77A:9 [Time Travel]
    TimeEnd          : 77A:C [Time Travel]
    Function         : UnknownOrMissingSymbols
    FunctionAddress  : 0x7561ccc0
    ReturnAddress    : 0x6cf12406
    ReturnValue      : 0x0
    Parameters    
```

## <a name="filtering-in-a-query"></a>查询中的筛选

使用 Select （）方法可选择要查看和修改列显示名称的列。

此示例返回 ReturnValue 不为零的行，并选择显示具有自定义显示名称和错误的 TimeStart 和 ReturnValue 列。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })
@$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })                
    [0x13]          
        Time             : 3C64A:834 [Time Travel]
        Error            : 0x36b7
    [0x1c]          
        Time             : 3B3E7:D6 [Time Travel]
        Error            : 0x3f0
    [0x1d]          
        Time             : 3C666:857 [Time Travel]
        Error            : 0x36b7
    [0x20]          
        Time             : 3C67E:12D [Time Travel]
```

## <a name="grouping"></a>分组

使用 GroupBy （）方法对查询返回的数据进行分组，以使用结构化结果执行分析。此示例按错误号对时间位置进行分组。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue }).GroupBy(x => x.Error)
@$s = @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue }).GroupBy(x => x.Error)                
    [0x36b7]        
        [0x0]           
        [0x1]           
        [0x2]           
        [0x3]           
        [...]           
    [0x3f0]         
        [0x0]           
        [0x1]           
        [0x2]           
        [0x3]           
...
```

## <a name="assigning-result-of-a-query-to-a-variable"></a>将查询结果赋给变量

使用此语法可以将查询的结果分配给变量 `dx @$var = <expression>`

此示例将查询的结果分配给 myResults

```dbgcmd
dx -r2 @$myResults = @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })
```

使用 dx 命令可使用-g 网格选项显示新创建的变量。 有关 dx 命令选项的详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

```dbgcmd
0:000> dx -g @$myResults
========================================
=           = (+) Time     = (+) Error =
========================================
= [0x13]    - 3C64A:834    - 0x36b7    =
= [0x1c]    - 3B3E7:D6     - 0x3f0     =
= [0x1d]    - 3C666:857    - 0x36b7    =
= [0x20]    - 3C67E:12D    - 0x2       =
= [0x21]    - 3C6F1:127    - 0x2       =
= [0x23]    - 3A547:D6     - 0x3f0     =
= [0x24]    - 3A59B:D0     - 0x3f0     =
```


## <a name="examples"></a>示例

### <a name="querying-for-exceptions"></a>查询异常

此 LINQ 查询使用[TTD。](time-travel-debugging-event-objects.md)用于显示跟踪中的所有异常的事件对象。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
@$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
    [0x0]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x1]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x2]            : Exception 0xE06D7363 of type CPlusPlus at PC: 0X777F51D0
```

### <a name="querying-for-specific-api-calls"></a>查询特定的 API 调用

请使用[TTD。调用对象](time-travel-debugging-calls-objects.md)以查询特定的 API 调用。 在此示例中，调用 user32 时出错 *！MessageBoxW*，WINDOWS API 用于显示消息框。 我们列出了对 MessageBoxW 的所有调用，按函数的开始时间对其进行排序，然后选择最后一个调用。

```dbgcmd
0:000> dx @$cursession.TTD.Calls("user32!MessageBoxW").OrderBy(c => c.TimeStart).Last()
@$cursession.TTD.Calls("user32!MessageBoxW").OrderBy(c => c.TimeStart).Last()                
    EventType        : Call
    ThreadId         : 0x3a10
    UniqueThreadId   : 0x2
    TimeStart        : 458310:539 [Time Travel]
    TimeEnd          : 45C648:61 [Time Travel]
    Function         : UnknownOrMissingSymbols
    FunctionAddress  : 0x750823a0
    ReturnAddress    : 0x40cb93
    ReturnValue      : 0x10a7000000000001
    Parameters

```

### <a name="querying-for-the-load-event-of-a-specific-module"></a>查询特定模块的 load 事件

首先，使用 " [lm （列表加载的模块）](lm--list-loaded-modules-.md) " 命令显示已加载的模块。

```dbgcmd
0:000> lm
start    end        module name
012b0000 012cf000   CDog_Console   (deferred)             
11570000 1158c000   VCRUNTIME140D   (deferred)             
11860000 119d1000   ucrtbased   (deferred)             
119e0000 11b63000   TTDRecordCPU   (deferred)             
11b70000 11cb1000   TTDWriter   (deferred)             
73770000 73803000   apphelp    (deferred)             
73ea0000 74062000   KERNELBASE   (deferred)             
75900000 759d0000   KERNEL32   (deferred)             
77070000 771fe000   ntdll      (private pdb symbols)
```

然后，使用以下 dx 命令查看特定模块的加载位置（如 ntdll.dll）。

```dbgcmd
dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Loaded at position: A:0 
```

此 LINQ 查询显示特定模块的加载事件。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Unloaded at position: FFFFFFFFFFFFFFFE:0
```
FFFFFFFFFFFFFFFE 的地址：0指示跟踪的结束。 



### <a name="querying-for-all-of-the-error-checks-in-the-trace"></a>查询跟踪中的所有错误检查

使用此命令按错误计数在跟踪中按所有错误检查进行排序。

```dbgcmd
0:000> dx -g @$cursession.TTD.Calls("kernelbase!GetLastError").Where( x=> x.ReturnValue != 0).GroupBy(x => x.ReturnValue).Select(x => new { ErrorNumber = x.First().ReturnValue, ErrorCount = x.Count()}).OrderByDescending(p => p.ErrorCount),d
==================================================
=                 = (+) ErrorNumber = ErrorCount =
==================================================
= [1008]          - 1008            - 8668       =
= [14007]         - 14007           - 4304       =
= [2]             - 2               - 1710       =
= [6]             - 6               - 1151       =
= [1400]          - 1400            - 385        =
= [87]            - 87              - 383        =
```

### <a name="querying-for-the-time-position-in-the-trace-when-threads-were-created"></a>在创建线程时查询跟踪中的时间位置

使用此 dx 命令以网格格式（-g）显示跟踪中的所有事件。

```dbgcmd
0:000> dx -g @$curprocess.TTD.Events
==================================================================================================================================================================================================
=                                                          = (+) Type            = (+) Position          = (+) Module                                                   = (+) Thread             =
==================================================================================================================================================================================================
= [0x0] : Module Loaded at position: 2:0                   - ModuleLoaded        - 2:0                   - Module C:\Users\USER1\Documents\Visual Studio 2015\Proje... -                        =
= [0x1] : Module Loaded at position: 3:0                   - ModuleLoaded        - 3:0                   - Module C:\WINDOWS\SYSTEM32\VCRUNTIME140D.dll at address 0... -                        =
= [0x2] : Module Loaded at position: 4:0                   - ModuleLoaded        - 4:0                   - Module C:\WINDOWS\SYSTEM32\ucrtbased.dll at address 0X118... -                        =
= [0x3] : Module Loaded at position: 5:0                   - ModuleLoaded        - 5:0                   - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x4] : Module Loaded at position: 6:0                   - ModuleLoaded        - 6:0                   - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x5] : Module Loaded at position: 7:0                   - ModuleLoaded        - 7:0                   - Module C:\WINDOWS\SYSTEM32\apphelp.dll at address 0X73770... -                        =
= [0x6] : Module Loaded at position: 8:0                   - ModuleLoaded        - 8:0                   - Module C:\WINDOWS\System32\KERNELBASE.dll at address 0X73... -                        =
= [0x7] : Module Loaded at position: 9:0                   - ModuleLoaded        - 9:0                   - Module C:\WINDOWS\System32\KERNEL32.DLL at address 0X7590... -                        =
= [0x8] : Module Loaded at position: A:0                   - ModuleLoaded        - A:0                   - Module C:\WINDOWS\SYSTEM32\ntdll.dll at address 0X7707000... -                        =
= [0x9] : Thread created at D:0                            - ThreadCreated       - D:0                   -                                                              - UID: 2, TID: 0x4C2C    =
= [0xa] : Thread terminated at 64:0                        - ThreadTerminated    - 64:0                  -                                                              - UID: 2, TID: 0x4C2C    =
= [0xb] : Thread created at 69:0                           - ThreadCreated       - 69:0                  -                                                              - UID: 3, TID: 0x4CFC    =
= [0xc] : Thread created at 6A:0                           - ThreadCreated       - 6A:0                  -                                                              - UID: 4, TID: 0x27B0    =
= [0xd] : Thread terminated at 89:0                        - ThreadTerminated    - 89:0                  -                                                              - UID: 4, TID: 0x27B0    =
= [0xe] : Thread terminated at 8A:0                        - ThreadTerminated    - 8A:0                  -                                                              - UID: 3, TID: 0x4CFC    =
= [0xf] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0  - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\Users\USER1\Documents\Visual Studio 2015\Proje... -                        =
= [0x10] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x11] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\VCRUNTIME140D.dll at address 0... -                        =
= [0x12] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\Users\USER1\AppData\Local\Dbg\UI\Fast.20170907... -                        =
= [0x13] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\ucrtbased.dll at address 0X118... -                        =
= [0x14] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\apphelp.dll at address 0X73770... -                        =
= [0x15] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\System32\KERNELBASE.dll at address 0X73... -                        =
= [0x16] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\System32\KERNEL32.DLL at address 0X7590... -                        =
= [0x17] : Module Unloaded at position: FFFFFFFFFFFFFFFE:0 - ModuleUnloaded      - FFFFFFFFFFFFFFFE:0    - Module C:\WINDOWS\SYSTEM32\ntdll.dll at address 0X7707000... -                        =
==================================================================================================================================================================================================
```

单击带有 + 号的任何列以对输出进行排序。

使用此 LINQ 查询以网格格式显示，在创建线程时跟踪跟踪中的时间位置（键入 = = "ThreadCreated"）。

```dbgcmd
dx -g @$curprocess.TTD.Events.Where(t => t.Type == "ThreadCreated").Select(t => t.Thread) 
===========================================================================================================
=                             = (+) UniqueId = (+) Id    = (+) Lifetime                 = (+) ActiveTime  =
===========================================================================================================
= [0x0] : UID: 2, TID: 0x4C2C - 0x2          - 0x4c2c    - [0:0, FFFFFFFFFFFFFFFE:0]    - [D:0, 64:0]     =
= [0x1] : UID: 3, TID: 0x4CFC - 0x3          - 0x4cfc    - [0:0, 8A:0]                  - [69:0, 8A:0]    =
= [0x2] : UID: 4, TID: 0x27B0 - 0x4          - 0x27b0    - [0:0, 89:0]                  - [6A:0, 89:0]    =
===========================================================================================================
```

使用此 LINQ 查询以网格格式显示，当线程终止时跟踪跟踪中的时间位置（Type = = "ThreadTerminated"）。

```dbgcmd
0:000> dx -g @$curprocess.TTD.Events.Where(t => t.Type == "ThreadTerminated").Select(t => t.Thread) 
===========================================================================================================
=                             = (+) UniqueId = (+) Id    = (+) Lifetime                 = (+) ActiveTime  =
===========================================================================================================
= [0x0] : UID: 2, TID: 0x4C2C - 0x2          - 0x4c2c    - [0:0, FFFFFFFFFFFFFFFE:0]    - [D:0, 64:0]     =
= [0x1] : UID: 4, TID: 0x27B0 - 0x4          - 0x27b0    - [0:0, 89:0]                  - [6A:0, 89:0]    =
= [0x2] : UID: 3, TID: 0x4CFC - 0x3          - 0x4cfc    - [0:0, 8A:0]                  - [69:0, 8A:0]    =
===========================================================================================================
```

### <a name="sorting-output-to-determine-the-longest-running-threads"></a>对输出进行排序以确定运行时间最长的线程

使用此 LINQ 查询可在跟踪中以网格格式显示大致时间最长的运行线程。

```dbgcmd
0:000> dx -g @$curprocess.TTD.Events.Where(e => e.Type == "ThreadTerminated").Select(e => new { Thread = e.Thread, ActiveTimeLength = e.Thread.ActiveTime.MaxPosition.Sequence - e.Thread.ActiveTime.MinPosition.Sequence }).OrderByDescending(t => t.ActiveTimeLength)
=========================================================
=          = (+) Thread              = ActiveTimeLength =
=========================================================
= [0x0]    - UID: 2, TID: 0x1750     - 0x364030         =
= [0x1]    - UID: 3, TID: 0x420C     - 0x360fd4         =
= [0x2]    - UID: 7, TID: 0x352C     - 0x35da46         =
= [0x3]    - UID: 9, TID: 0x39F4     - 0x34a5b5         =
= [0x4]    - UID: 11, TID: 0x4288    - 0x326199         =
= [0x5]    - UID: 13, TID: 0x21C8    - 0x2fa8d8         =
= [0x6]    - UID: 14, TID: 0x2188    - 0x2a03e3         =
= [0x7]    - UID: 15, TID: 0x40E8    - 0x29e7d0         =
= [0x8]    - UID: 16, TID: 0x124     - 0x299677         =
= [0x9]    - UID: 4, TID: 0x2D74     - 0x250f43         =
= [0xa]    - UID: 5, TID: 0x2DC8     - 0x24f921         =
= [0xb]    - UID: 6, TID: 0x3B1C     - 0x24ec8e         =
= [0xc]    - UID: 10, TID: 0x3808    - 0xf916f          =
= [0xd]    - UID: 12, TID: 0x26B8    - 0x1ed3a          =
= [0xe]    - UID: 17, TID: 0x37D8    - 0xc65            =
= [0xf]    - UID: 8, TID: 0x45F8     - 0x1a2            =
=========================================================
```

### <a name="querying-for-read-accesses-to-a-memory-range"></a>查询对内存范围的读访问 

请使用[TTD。](time-travel-debugging-memory-objects.md)用于查询以查询对内存范围的读取访问的内存对象。

线程环境块（TEB）是一个结构，其中包含有关线程状态的所有信息，包括 GetLastError （）返回的结果。 您可以通过为当前线程运行 `dx @$teb` 来查询此数据结构。 TEB 的成员之一是 LastErrorValue 变量，大小为4个字节。 使用此语法，可以引用 TEB 中的 LastErrorValue 成员。 `dx &@$teb->LastErrorValue`。

示例查询显示了如何在内存中查找在该范围内完成的每个读取操作，选择在创建对话框之前发生的所有读取，然后对结果进行排序以查找上次读取操作。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
@$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]     
```

如果在跟踪中发生了 "对话" 事件，则可以运行查询来查找在内存中该范围内完成的每个读取操作，选择创建该对话框之前发生的所有读取，然后对结果进行排序以查找上次读取操作。 然后，通过在生成的时间位置调用 SeekTo （），将时间移动到该时间点。

```dbgcmd

:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r").Where(m => m.TimeStart < @$dialog).OrderBy(m => m.TimeStart).Last().TimeEnd.SeekTo()
Setting position: 458300:37
ModLoad: 6cee0000 6cf5b000   C:\WINDOWS\system32\uxtheme.dll
ModLoad: 75250000 752e6000   C:\WINDOWS\System32\OLEAUT32.dll
ModLoad: 76320000 7645d000   C:\WINDOWS\System32\MSCTF.dll
ModLoad: 76cc0000 76cce000   C:\WINDOWS\System32\MSASN1.dll
```

## <a name="github-ttd-query-lab"></a>GitHub TTD 查询实验室

有关如何使用时间行程调试记录C++调试代码的教程，请参阅使用查询查找有关如何执行有问题的代码的信息的详细信息，请参阅 https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md 。

实验室中使用的所有代码都可在此处找到： https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample 。


## <a name="troubleshooting-ttd-queries"></a>TTD 查询故障排除

### <a name="unknownormissingsymbols-as-the-function-names"></a>"UnknownOrMissingSymbols" 作为函数名称

数据模型扩展需要完整的符号信息才能提供函数名称、参数值等。当不能使用完整符号信息时，调试器会使用 "UnknownOrMissingSymbols" 作为函数名称。

- 如果有私有符号，将获得函数名称和正确的参数列表。
- 如果拥有公共符号，则将获得函数名称和默认的参数集-四个无符号64位整数。
- 如果你正在查询的模块没有符号信息，则使用 "UnknownOrMissingSymbols" 作为名称。

### <a name="ttd-queries-for-calls"></a>调用的 TTD 查询

查询不会返回任何内容来调用 DLL，这可能有多种原因。

- 调用的语法不是很正确。  尝试使用 x 命令验证调用语法： "x <call>"。 如果 x 返回的模块名称采用大写形式，则使用该名称。
- DLL 尚未加载，稍后会在跟踪中加载。 若要解决此情况，请在加载 DLL 后的某个时间点执行此操作，然后重做查询。
- 调用是内联的，查询引擎无法跟踪。
- 查询模式使用返回太多函数的通配符。  请尝试使该查询模式更为具体，使匹配函数的数量足够小。

## <a name="see-also"></a>另请参阅

[将 LINQ 用于调试器对象](using-linq-with-the-debugger-objects.md)

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[行程调试-概述](time-travel-debugging-overview.md)

[行程调试-JavaScript 自动化](time-travel-debugging-javascript-automation.md)

---
