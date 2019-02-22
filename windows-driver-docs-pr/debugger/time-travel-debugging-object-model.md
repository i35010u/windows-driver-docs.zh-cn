---
title: 时间旅行调试-时间旅行调试对象简介
description: 本部分介绍如何使用将数据模型与查询时传输跟踪。
ms.date: 12/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9089354463db0e453866b25ba6d626b7c33595e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540724"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png) 

# <a name="introduction-to-time-travel-debugging-objects"></a>时间旅行调试对象简介
本部分介绍如何使用将数据模型与查询时传输跟踪。 这可以是一个强大的工具来回答以下有关时间旅行跟踪中捕获的代码问题。
* 在跟踪中有哪些异常？
* 在的跟踪中的时间点的特定代码模块加载吗？
* 何时线程创建/终止在跟踪中？

将数据添加到的 TTD 扩展有*会话*并*进程*数据模型对象。 模型对象可以通过访问`dx`，WinDbg 预览模型 windows 和 JavaScript。 这两个这些扩展会自动加载调试时间旅行跟踪时。

## <a name="process-objects"></a>处理对象
添加到的主对象*进程*中可以找到对象*TTD*命名空间从任何*过程*对象。 例如， `@$curprocess.TTD`。

### <a name="properties"></a>属性

| 对象 | 描述 |
| --- | --- |
| 生存期 | 一个[TTD 范围对象](time-travel-debugging-range-objects.md)描述整个跟踪的生存期。 |
| 线程 | 包含一系列[TTD 线程对象](time-travel-debugging-thread-objects.md)，一个用于每个线程的整个生存期内跟踪。 |
| 事件 | 包含一系列[TTD 事件对象](time-travel-debugging-event-objects.md)，一个用于在跟踪中的每个事件。 |

### <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| SetPosition() | 介于 0 和 100 或字符串之间的整数采用 N:N 窗体作为输入并跟踪将跳转到该位置。 请参阅[！ tt](time-travel-debugging-extension-tt.md)有关详细信息。|

## <a name="session-objects"></a>会话对象
添加到的主对象*会话*中可以找到对象*TTD*命名空间从任何*会话*对象。 例如， `@$cursession.TTD`。

> [!NOTE]
> 有一些对象和由 TTDAnalyze 添加用于扩展的内部函数的方法。 记录不是所有命名空间和当前的命名空间将随时间发展。 
>

### <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| Data.Heap() | 一系列[堆对象](time-travel-debugging-heap-objects.md)在跟踪期间分配。 请注意，这是执行计算，因此需要一段时间才能运行的函数。|
| Calls() | 返回的集合[调用对象](time-travel-debugging-calls-objects.md)与输入的字符串相匹配。 输入的字符串可以包含通配符。 请注意，这是执行计算，因此需要一段时间才能运行的函数。  |
| Memory() | 这是一种方法接受 beginAddress、 endAddress 和 dataAccessMask 参数并返回一系列[内存对象](time-travel-debugging-memory-objects.md)。 请注意，这是执行计算，因此需要一段时间才能运行的函数。  |



## <a name="examples"></a>示例

### <a name="querying-for-exceptions"></a>查询异常

此 LINQ 查询将显示在跟踪中的所有异常。

```dbgcmd
dx @$curprocess.TTD.Events.Where(t => t.Type == "Exception").Select(e => e.Exception) 
```

### <a name="querying-for-the-load-event-of-a-specific-module"></a>查询特定模块的加载事件

使用[lm （列表加载模块）](lm--list-loaded-modules-.md)命令以显示已加载的模块。

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

然后使用以下 dx 命令以查看在跟踪中的哪个位置加载特定模块。

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





## <a name="see-also"></a>另请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

[按照时间顺序逐个调试-JavaScript 自动化](time-travel-debugging-javascript-automation.md)

---





