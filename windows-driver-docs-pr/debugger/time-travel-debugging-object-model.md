---
title: 时光穿越调试 - 时光穿越调试对象简介
description: 本部分介绍如何使用将数据模型与查询时传输跟踪。
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1dda35dc8ce9f7da77c0abeb06446969feb97c98
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903615"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

# <a name="introduction-to-time-travel-debugging-objects"></a>时间旅行调试对象简介
本部分介绍如何使用将数据模型与查询时传输跟踪。 这可以是一个强大的工具来回答以下有关时间旅行跟踪中捕获的代码问题。
* 在跟踪中有哪些异常？
* 在的跟踪中的时间点的特定代码模块加载吗？
* 何时线程创建/终止在跟踪中？
* 在跟踪中的运行时间最长线程有哪些？

将数据添加到的 TTD 扩展有*会话*并*进程*数据模型对象。 可以通过访问 TTD 数据模型对象[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)命令时，模型 windows 的 WinDbg 预览版，JavaScript 和C++。 调试时间旅行跟踪时，会自动加载 TTD 扩展。

## <a name="process-objects"></a>处理对象

添加到的主对象*进程*中可以找到对象*TTD*命名空间从任何*过程*对象。 例如，`@$curprocess.TTD`。

```dbgcmd
:000> dx @$curprocess.TTD
@$curprocess.TTD                
    Threads         
    Events          
    Lifetime         : [26:0, 464232:0]
    SetPosition      [Sets the debugger to point to the given position on this process.]
```

有关使用 LINQ 查询和调试器对象的常规信息，请参阅[使用调试器对象与 LINQ](using-linq-with-the-debugger-objects.md)。

### <a name="properties"></a>属性

| Object | 描述 |
| --- | --- |
| 生存期 | 一个[TTD 范围对象](time-travel-debugging-range-objects.md)描述整个跟踪的生存期。 |
| 线程 | 包含一系列[TTD 线程对象](time-travel-debugging-thread-objects.md)，一个用于每个线程的整个生存期内跟踪。 |
| 事件 | 包含一系列[TTD 事件对象](time-travel-debugging-event-objects.md)，一个用于在跟踪中的每个事件。 |

### <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| SetPosition() | 介于 0 和 100 或字符串之间的整数采用 N:N 窗体作为输入并跟踪将跳转到该位置。 请参阅[！ tt](time-travel-debugging-extension-tt.md)有关详细信息。|

## <a name="session-objects"></a>会话对象
添加到的主对象*会话*中可以找到对象*TTD*命名空间从任何*会话*对象。 例如，`@$cursession.TTD`。

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
> 有一些对象和由 TTDAnalyze 添加用于扩展的内部函数的方法。 并非所有命名空间记录，并且当前的命名空间将随时间发展。
>

### <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| Data.Heap() | 一系列[堆对象](time-travel-debugging-heap-objects.md)在跟踪期间分配。 请注意，这是执行计算，因此需要一段时间才能运行的函数。|
| Calls() | 返回的集合[调用对象](time-travel-debugging-calls-objects.md)与输入的字符串相匹配。 输入的字符串可以包含通配符。 请注意，这是执行计算，因此需要一段时间才能运行的函数。  |
| Memory() | 这是一种方法接受 beginAddress、 endAddress 和 dataAccessMask 参数并返回一系列[内存对象](time-travel-debugging-memory-objects.md)。 请注意，这是执行计算，因此需要一段时间才能运行的函数。  |


## <a name="sorting-query-output"></a>排序的查询输出

使用 orderby （） 方法从查询返回的一个或多个列的行进行排序。 此示例对 TimeStart 排序升序排序。

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

若要显示的数据模型对象的更深入了解-r2 递归级别选项使用。 有关 dx 命令选项的详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

此示例对 TimeStart 排序降序排序。

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

## <a name="specifying-elements-in-a-query"></a>在查询中指定元素

若要选择的特定元素的限定符各种可以追加到查询。 例如，查询会显示包含"kernelbase 第一次调用 ！GetLastError"。

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

## <a name="filtering-in-a-query"></a>在查询中进行筛选

Select （） 方法用于选择要查看和修改列的列显示名称。

此示例返回其中 ReturnValue 不为零，并且选择要显示的时间和错误的自定义显示名称的 TimeStart 和 ReturnValue 列中的行。

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

Groupby （） 方法用于按错误编号的时间位置返回的查询执行使用结构化的结果分析此示例将分组的数据进行分组。

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

## <a name="assigning-result-of-a-query-to-a-variable"></a>将查询的结果分配给一个变量

使用此语法来查询的结果分配给变量 `dx @$var = <expression>`

此示例将查询的结果分配给 myResults

```dbgcmd
dx -r2 @$myResults = @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0).Select(c => new { Time = c.TimeStart, Error = c.ReturnValue })
```

使用 dx 命令显示新创建的变量使用-g 网格选项。 Dx 命令选项的详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

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

此 LINQ 查询使用[TTD。事件对象](time-travel-debugging-event-objects.md)要在跟踪中显示的所有异常。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
@$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception)
    [0x0]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x1]            : Exception 0x000006BA of type Software at PC: 0X777F51D0
    [0x2]            : Exception 0xE06D7363 of type CPlusPlus at PC: 0X777F51D0
```

### <a name="querying-for-specific-api-calls"></a>查询特定的 API 调用

使用[TTD。调用对象](time-travel-debugging-calls-objects.md)查询特定的 API 调用。 在此示例中，错误发生时调用*user32 ！MessageBoxW*，Windows API 来显示一个消息框。 我们列出所有调用的 MessageBoxW，该函数的开始时间排序，然后挑选最后一次调用。

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

### <a name="querying-for-the-load-event-of-a-specific-module"></a>查询特定模块的加载事件

首先，使用[lm （列表加载模块）](lm--list-loaded-modules-.md)命令以显示已加载的模块。

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

然后使用以下 dx 命令以查看在跟踪中的哪个位置特定已加载模块，如 ntdll。

```dbgcmd
dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleLoaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Loaded at position: A:0 
```

此 LINQ 查询显示为特定模块加载事件。

```dbgcmd
0:000> dx @$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll")) 
@$curprocess.TTD.Events.Where(t => t.Type == "ModuleUnloaded").Where(t => t.Module.Name.Contains("ntdll.dll"))                 
    [0x0]            : Module Unloaded at position: FFFFFFFFFFFFFFFE:0
```
FFFFFFFFFFFFFFFE:0 的地址指示跟踪的末尾。 



### <a name="querying-for-all-of-the-errors-in-the-trace"></a>在跟踪中的错误的所有查询

使用此命令通过错误计数按所有在跟踪中的错误进行排序。

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

### <a name="querying-for-the-time-position-in-the-trace-when-threads-were-created"></a>创建线程时查询在跟踪中的时间位置

使用此 dx 命令中以网格格式在跟踪中显示的所有事件 (-g)。

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

任何具有的列上单击 + 号的输出进行排序。

创建线程时使用此 LINQ 查询为以网格格式显示，则在跟踪中的时间位置 (类型 = ="ThreadCreated")。

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

线程已终止时，使用网格格式显示，则在跟踪中的时间位置到此 LINQ 查询 (类型 = ="ThreadTerminated")。

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

### <a name="sorting-output-to-determine-the-longest-running-threads"></a>排序输出，以确定最长正在运行的线程

使用此 LINQ 查询为以网格格式显示，则在跟踪中的近似最长运行线程。

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

### <a name="querying-for-read-accesses-to-a-memory-range"></a>查询对内存范围的读取访问 

使用[TTD。内存对象](time-travel-debugging-memory-objects.md)进行查询的查询读取访问都指向内存范围。

线程环境块 (TEB) 是一种结构，其中包含有关状态的线程的所有信息，包括结果返回 getlasterror （）。 可以通过运行查询此数据结构`dx @$teb`当前线程。 TEB 成员之一是 LastErrorValue 变量，大小为 4 个字节。 我们可以引用中使用此语法 TEB LastErrorValue 成员。 `dx &@$teb->LastErrorValue`。

示例查询演示如何查找该范围中的内存来完成每个读取的操作，请选择之前发生的所有读取一个对话框已创建，然后对要查找最后一个读取操作的结果进行排序。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
@$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r")
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]     
```

如果我们跟踪中的"对话框"事件已的发生我们可以运行查询来查找该范围中的内存来完成每个读取的操作，选择发生之前已创建对话框，然后对要查找最后一个读取操作的结果进行排序的所有读取。 然后通过调用结果的时间位置 SeekTo() 时间前往该点时间。

```dbgcmd

:000> dx @$cursession.TTD.Memory(&@$teb->LastErrorValue, &@$teb->LastErrorValue + 0x4, "r").Where(m => m.TimeStart < @$dialog).OrderBy(m => m.TimeStart).Last().TimeEnd.SeekTo()
Setting position: 458300:37
ModLoad: 6cee0000 6cf5b000   C:\WINDOWS\system32\uxtheme.dll
ModLoad: 75250000 752e6000   C:\WINDOWS\System32\OLEAUT32.dll
ModLoad: 76320000 7645d000   C:\WINDOWS\System32\MSCTF.dll
ModLoad: 76cc0000 76cce000   C:\WINDOWS\System32\MSASN1.dll
```

## <a name="github-ttd-query-lab"></a>GitHub TTD 查询实验室

有关如何调试的教程C++使用时间旅行调试记录使用查询查找有问题的代码的执行有关的信息有问题，请参阅代码 https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md。

所有在实验室中使用的代码位于此处： https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample。


## <a name="troubleshooting-ttd-queries"></a>故障排除 TTD 查询

### <a name="unknownormissingsymbols-as-the-function-names"></a>"UnknownOrMissingSymbols"作为函数名称

数据模型扩展插件所需的完整符号信息提供的函数名称、 参数值，等等。完整符号信息不可用时，调试器使用"UnknownOrMissingSymbols"作为函数名称。

- 如果你将获取函数名称和参数的正确列表的私有符号。
- 如果你将获取函数名称和一组默认的参数-四个无符号 64 位整数的公共符号。
- 如果您有没有对应符号信息所查询的模块，然后"UnknownOrMissingSymbols"用作名称。

### <a name="ttd-queries-for-calls"></a>调用的 TTD 查询

可以有多种原因，查询不返回任何内容对 DLL 的调用。

- 调用的语法不太好。  请尝试使用 x 命令验证的调用语法:"x <call>"。 返回模块名称 x 是否以大写形式，使用它。
- DLL 加载尚未并不会加载更高版本中的跟踪。 若要解决此前往点在之后加载了 DLL 的时间和重复查询。
- 调用是内联查询引擎是无法跟踪。
- 查询模式是使用通配符，它将返回过多的函数。  尝试使查询模式，以便匹配功能的数量很少，足以更具针对性。

## <a name="see-also"></a>请参阅

[使用 LINQ 与调试器对象](using-linq-with-the-debugger-objects.md)

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

[按照时间顺序逐个调试-JavaScript 自动化](time-travel-debugging-javascript-automation.md)

---