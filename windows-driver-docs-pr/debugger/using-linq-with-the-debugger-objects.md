---
title: 将 LINQ 与调试器对象配合使用
description: 将 LINQ 与调试器对象一起使用。 LINQ 语法可以与调试器对象结合使用来搜索和操作数据。
keywords:
- 将 LINQ 与调试器对象配合使用
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 14e3adaee50d25d283513cc3befef4c6ad8658a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834204"
---
# <a name="using-linq-with-the-debugger-objects"></a>将 LINQ 与调试器对象配合使用

LINQ 语法可以与调试器对象结合使用来搜索和操作数据。 将 LINQ 语法与 dx 命令结合使用，可实现与使用调试器命令更一致的体验。 无论正在查看哪个调试器对象，输出和选项都是一致的。 LINQ 查询允许您提出一些问题，例如 "运行最多线程的前5个进程是什么？"。

调试器对象投影到以 "调试器" 为根的命名空间中。 进程、模块、线程、堆栈、堆栈帧和局部变量均可在 LINQ 查询中使用。

LINQ 在概念上类似于用于查询数据库的结构化查询语言（SQL）。 可以使用多个 LINQ 方法搜索、筛选和分析调试数据。 使用 LINQ C#方法语法。 有关 LINQ 和 LINQ C#语法的详细信息，请参阅[中的入门 linq C# in](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/getting-started-with-linq)

调试器支持中使用的 LINQ 使用 LINQ 的 "方法语法"，而不是 "查询语法"。 可以在[LINQ （语言集成查询）](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)中找到有关差异的详细信息。

LINQ 命令（如下所示）可与调试器对象一起使用。 All、。Any、。计数、。首先，。平展，。GroupBy，。Last。OrderBy，。OrderByDescending、。选择 "与"。其中. 这些方法遵循C# LINQ 方法窗体。

## <a name="native-debugger-objects"></a>本机调试器对象

本机调试器对象表示调试器环境的各种构造和行为。 示例调试器对象包括以下各项。

- 会议
- 线程/线程
- 进程/进程
- 堆栈帧/堆栈帧
- 局部变量
- 模块/模块
- 实用程序
- 省/市/自治区
- “设置”

还可以使用 NatVis 处理调试器对象。 有关详细信息，请参阅[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)。 有关将调试器对象与 JavaScript 一起使用的信息，请参阅[Javascript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。 有关使用C++和驱动程序对象的信息，请参阅[调试器数据模型C++概述](data-model-cpp-overview.md)。

## <a name="dx-command"></a>Dx 命令

此处显示的示例使用 dx 命令，有关使用 dx 命令的详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

## <a name="developing-a-linq-query"></a>开发 LINQ 查询

开发 LINQ 调试器对象查询的一种方法是使用显示的 DML 链接来浏览数据模型，以首先查找将在查询中使用的调试器对象。

在此示例中，我们想要显示内核调试会话中的进程列表，以及每个进程的线程数。

若要开始我们的探索，可以使用 dx 命令显示顶级调试器对象。

```dbgcmd
0: kd> dx Debugger
Debugger
    Sessions
    Settings
    State
    Utility
```

单击顶级主题后，我们确定会话看起来最有趣，因此，单击 DML 链接即可显示它包含*进程*。 

```dbgcmd
0: kd> dx -r1 Debugger.Sessions[0]
Debugger.Sessions[0]                 : Remote KD: KdSrv:Server=@{<Local>},Trans=@{NET:Port=50005,Key=MyKey}
    Processes
    Id               : 0
    Attributes
```

然后，单击 "下一步" 以查看特定进程，并发现与该进程关联的*线程*可用。 单击其中一个进程的*线程*时，将看到与该进程关联的所有线程都可用。


```dbgcmd
0: kd> dx -r1 Debugger.Sessions[0].Processes[1428].Threads
Debugger.Sessions[0].Processes[1428].Threads
    [0x598]          : <Unable to get stack trace> [Switch To]
    [0x1220]         : <Unable to get stack trace> [Switch To]
    [0x6f8]          : nt!KiSwapContext+0x76 (fffff806`4466a186)  [Switch To]
    [0x128c]         : <Unable to get stack trace> [Switch To]
    [0x27e4]         : nt!KiSwapContext+0x76 (fffff806`4466a186)  [Switch To] 
```

现在，我们知道，在调试器对象模型中提供了显示与进程关联的线程数所需的数据。

为了使 LINQ 查询更短一些，可以使用本主题后面介绍的[系统定义变量](#system-defined-variables)来显示与当前会话关联的进程。

```dbgcmd
0: kd> dx @$cursession.Processes
@$cursession.Processes                
    [0x0]            : Idle [Switch To]
    [0x4]            : System [Switch To]
    [0x90]           : Registry [Switch To]
...
```

接下来，添加 select 语句。 首先，可以指定名称字段。

```dbgcmd
0: kd> dx @$cursession.Processes.Select(p => p.Name)
@$cursession.Processes.Select(p => p.Name)                
    [0x0]            : Idle
    [0x4]            : System
    [0x90]           : Registry
...
```

对于我们的方案，还需要线程数。 因为有两个字段，所以请使用*new*（类似于C#下面的[用户定义变量](#user-defined-variables)中所述的匿名类型语法）创建匿名类型。

```dbgcmd
dx @$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})
```

通过该命令，"dx" 实际上不会再输出该名称，因此，add-r2 （递归两个级别）用于显示名称和线程。

```dbgcmd
dx -r2 @$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})
@$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})                
    [0x0]           
        Name             : Idle
        Threads         
    [0x4]           
        Name             : System
        Threads         
    [0x90]          
        Name             : Registry
        Threads       
```

此时，我们将显示进程的名称和线程的列表。 若要显示 ThreadCount，请使用 *。Count （）* 方法。


```dbgcmd
0: kd> dx -r2 @$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()})
@$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()})                
    [0x0]           
        Name             : Idle
        ThreadCount      : 0x4
    [0x4]           
        Name             : System
        ThreadCount      : 0xe7
    [0x90]          
        Name             : Registry
        ThreadCount      : 0x4
...
```

若要查看哪些进程具有大量线程，请使用*OrderByDescending*按线程计数对列表排序。

```dbgcmd
0: kd> dx -r2 @$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()}).OrderByDescending(p => p.ThreadCount)
@$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()}).OrderByDescending(p => p.ThreadCount)                
    [0x4]           
        Name             : System
        ThreadCount      : 0xe7
    [0xa38]         
        Name             : svchost.exe
        ThreadCount      : 0x45
    [0x884]         
        Name             : MemCompression
        ThreadCount      : 0x3e
```

 若要在格式化的网格中呈现，请将 "-r2" 更改为 "-g"。 不需要指定递归级别，因为网格选项会相应地显示列。 最后，将 "，d" 格式说明符添加到输出小数值。

```dbgcmd
0: kd> dx -g @$cursession.Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count()}).OrderByDescending(p => p.ThreadCount),d
===========================================================================================
=            = Name                                                         = ThreadCount =
===========================================================================================
= [4]        - System                                                       - 231         =
= [2616]     - svchost.exe                                                  - 69          =
= [2180]     - MemCompression                                               - 62          =
= [968]      - explorer.exe                                                 - 61          =
```

## <a name="debugger-objects-examples"></a>调试器对象示例

此示例显示运行最多线程的前5个进程：

```dbgcmd
0: kd> dx -r2 Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5
Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5 

: 
    [0x4]            : 
        Name             : <Unknown Image>
        ThreadCount      : 0x73
    [0x708]          : 
        Name             : explorer.exe
        ThreadCount      : 0x2d
    [0x37c]          : 
        Name             : svchost.exe
        ThreadCount      : 0x2c
    [0x6b0]          : 
        Name             : MsMpEng.exe
        ThreadCount      : 0x22
    [0x57c]          : 
        Name             : svchost.exe
        ThreadCount      : 0x15
    [...]       
```

此示例显示了即插即用设备树中的设备，这些设备按物理设备对象驱动程序的名称进行分组。 不是所有输出都显示出来。

```dbgcmd
kd> dx -r2 Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString())
Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString()) 

: 
    ["\"\\Driver\\PnpManager\""] : 
        [0x0]            : HTREE\ROOT\0
        [0x1]            : ROOT\volmgr\0000 (volmgr)
        [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
        [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
        [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
         ...  
```

## <a name="dx-command-tab-auto-completion"></a>Dx 命令选项卡自动完成

上下文选项卡键自动完成功能可以识别 LINQ 查询方法，它们适用于 lambda 的参数。

例如，在调试器中键入（或复制并粘贴）以下文本。 然后多次按 TAB 键以循环执行可能的完成。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.
```

按 TAB 键直到 "。Name "。 添加右括号 "）"，并按 enter 执行该命令。

```dbgcmd
kd> dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name)
Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name) : 
    [0x274]          : 
        Name             : winlogon.exe
        ThreadCount      : 0x4
    [0x204]          : 
        Name             : wininit.exe
        ThreadCount      : 0x2
    [0x6c4]          : 
        Name             : taskhostex.exe
        ThreadCount      : 0x8
         ...  
```

此示例显示使用密钥比较运算符方法完成。 替换将显示字符串方法，因为键是一个字符串。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.
```

按 TAB 键直到 "。"长度" 显示。 添加右括号 "）"，并按 enter 执行该命令。

```dbgcmd
kd> dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.Length)
Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.Length) : 
    [0x544]          : 
        Name             : spoolsv.exe
        ThreadCount      : 0xc
    [0x4d4]          : 
        Name             : svchost.exe
        ThreadCount      : 0xa
    [0x438]          : 
        Name             : svchost.exe
```

## <a name="user-defined-variables"></a>用户定义的变量

可以通过在变量名称前加上 @ $ 来定义用户定义变量。 可以将用户定义的变量分配给 dx 可以使用的任何内容，例如 lambda、LINQ 查询的结果等。

你可以创建并设置用户变量的值，如下所示。

```dbgcmd
kd> dx @$String1="Test String"
```

可以使用*UserVariables*或 *@ $vars*显示定义的用户变量。

```dbgcmd
kd> dx Debugger.State.UserVariables
Debugger.State.UserVariables : 
    mySessionVar     : 
    String1          : Test String
```

您可以使用删除变量。取消.

```dbgcmd
kd> dx @$vars.Remove("String1")
```

此示例演示如何定义用户变量以引用 Sesssions。

```dbgcmd
kd> dx @$mySessionVar = Debugger.Sessions
```

然后，可以使用用户定义的变量，如下所示。

```dbgcmd
kd> dx -r2 @$mySessionVar 
@$mySessionVar   : 
    [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{COM:Port=\\.\com3,Baud=115200,Timeout=4000}
        Processes        : 
        Devices     
```
## <a name="system-defined-variables"></a>系统定义的变量

以下系统定义的变量可用于任何 LINQ dx 查询中。

-   @ $cursession-当前会话

-   @ $curprocess-当前进程

-   @ $curthread-当前线程

此示例演示如何使用系统定义的变量。

```dbgcmd
kd> dx @$curprocess.Threads.Count()
@$curprocess.Threads.Count() : 0x4
```

```dbgcmd
kd> dx -r1 @$curprocess.Threads
@$curprocess.Threads : 
    [0x4adc]         : 
    [0x1ee8]         : 
    [0x51c8]         : 
    [0x62d8]         : 
     ...
```

## <a name="user-defined-variables---anonymous-types"></a>用户定义的变量-匿名类型

动态对象的创建是使用C#匿名类型语法（new {...}）完成的。 有关详细信息，请参阅[匿名类型（C#编程指南）](https://docs.microsoft.com/dotnet/articles/csharp/programming-guide/classes-and-structs/anonymous-types)。 此示例创建一个具有整数和字符串值的匿名类型。

```dbgcmd
kd> dx -r1 new { MyInt = 42, MyString = "Hello World" }
new { MyInt = 42, MyString = "Hello World" } : 
    MyInt            : 42
    MyString         : Hello World
```


## <a name="function-objects-lambda-expressions"></a>函数对象（Lambda 表达式）

用于查询数据的许多方法都基于跨集合中的对象重复运行用户提供函数的概念。 为了支持在调试器中查询和操作数据的功能，dx 命令支持使用等效C#语法的 lambda 表达式。 Lambda 表达式由 =&gt; 运算符的用法定义，如下所示：

（arguments） =&gt; （result）

若要查看如何将 LINQ 与 dx 一起使用，请尝试使用这一简单示例将5和7相加。

```dbgcmd
kd> dx ((x, y) => (x + y))(5, 7) 
```

Dx 命令回显返回 lambda 表达式，并显示12的结果。

```dbgcmd
((x, y) => (x + y))(5, 7)  : 12
```

此示例 lambda 表达式结合了字符串 "Hello" 和 "World"。

```dbgcmd
kd> dx ((x, y) => (x + y))("Hello", "World")
((x, y) => (x + y))("Hello", "World") : HelloWorld
```


## <a name="supported-linq-syntax---query-methods"></a>支持的 LINQ 语法查询方法

Dx 定义为可迭代的任何对象（这是本机数组，NatVis 将其描述为容器或调试器扩展对象的类型）具有一系列 LINQ （或 LINQ 等效）方法。 这些查询方法如下所述。 查询方法的参数签名在所有查询方法之后列出。

筛选方法

|                            |                                                                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| .Where （PredicateMethod） | 返回一个新的对象集合，其中包含谓词方法为其返回 true 的输入集合中的每个对象。 |



投影方法

|                                     |                                                                                                                                                                                                                                                                                                                             |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .平展（\[KeyProjectorMethod\]） | 采用容器的输入容器（一个树），并将其平展到一个容器中，该容器具有树中的每个元素。 如果提供了可选的密钥投影仪方法，则会将树视为一个密钥容器，这些密钥是自身的容器，而这些密钥是通过调用投影方法确定的。 |
| .Select （KeyProjectorMethod）      | 返回一个新的对象集合，其中包含对输入集合中的每个对象调用投影仪方法的结果。                                                                                                                                                                                          |



分组方法

|                                                                                                                            |                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .GroupBy （KeyProjectorMethod、\[KeyComparatorMethod\]）                                                                   | 通过将输入集合中的所有对象与通过调用密钥投影仪方法确定的键组合在一起，返回集合的新集合。 可以提供可选的比较运算符方法。 |
| 联接（InnerCollection，外键选择器方法，内部键选择器方法，结果选择器方法，\[ComparatorMethod\]） | 基于键选择器函数联接两个序列并提取值对。 还可以指定可选的比较运算符方法。                                                                        |
| Intersect （InnerCollection，\[ComparatorMethod\]）                                                                          | 返回交集，这意味着出现在两个集合中的元素。 还可以指定可选的比较运算符方法。                                                               |
| 联合（InnerCollection、\[ComparatorMethod\]）                                                                              | 返回并集，这意味着在两个集合中的任何一个中出现的唯一元素。 还可以指定可选的比较运算符方法。                                                             |



数据集方法

|                                                |                                                                                                                                                                                                   |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Contains （Object，\[ComparatorMethod\]）        | 确定序列是否包含指定的元素。 可以提供一个可选的比较运算符方法，每次将元素与序列中的条目进行比较时，都会调用此方法。 |
| Distinct （\[ComparatorMethod\]）                | 从集合中移除重复值。 可以提供一个可选的比较运算符方法，以便每次必须对集合中的对象进行比较。                                      |
| Except （InnerCollection，\[ComparatorMethod\]） | 返回这两个集之间的差异，这意味着一个集合中未出现在第二个集合中的元素。 可以指定可选的比较运算符方法。                                 |
| Concat （InnerCollection）                       | 连接两个序列以形成一个序列。                                                                                                                                                  |



排序方法

|                                                                    |                                                                                                                                                                                                      |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .OrderBy （KeyProjectorMethod，\[KeyComparatorMethod\]）           | 根据通过对输入集合中的每个对象调用密钥投影方法提供的键，按升序对集合进行排序。 可以提供可选的比较运算符方法。  |
| .OrderByDescending （KeyProjectorMethod，\[KeyComparatorMethod\]） | 根据通过对输入集合中的每个对象调用密钥投影方法提供的键，按降序对集合进行排序。 可以提供可选的比较运算符方法。 |



聚合方法

|                            |                                                                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| Count （）                   | 返回集合中的元素数的方法。                                                                                |
| Sum （\[ProjectionMethod\]） | 计算集合中值的总和。 可以选择指定一个投影仪方法来转换元素，然后再进行求和。 |



Skip 方法

|                             |                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| Skip （计数）                | 跳过序列中指定位置的元素。                                      |
| SkipWhile （PredicateMethod） | 基于谓词函数跳过元素，直到元素不满足该条件。 |



Take 方法

|                             |                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| Take （计数）                | 获取序列中指定位置的元素。                                      |
| TakeWhile （PredicateMethod） | 根据谓词函数获取元素，直到元素不满足该条件。 |



比较方法

|                                                       |                                                                                                                                  |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| SequenceEqual （InnerCollection，\[ComparatorMethod\]） | 通过对元素进行成对比较来确定两个序列是否相等。 可以指定可选的比较运算符。 |



错误处理方法

|                                     |                                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------|
| AllNonError (PredicateMethod)       | 返回集合的所有非错误元素是否都满足给定的条件。 |
| FirstNonError （\[PredicateMethod\]） | 返回集合中不是错误的第一个元素。                    |
| LastNonError （\[PredicateMethod\]）  | 返回集合中不是错误的最后一个元素。                     |



其他方法

|                                |                                                                                                                                                                                                                                                                              |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .全部（PredicateMethod）       | 返回对输入集合中的每个元素调用指定谓词方法的结果是否为 true。                                                                                                                                                       |
| .Any （PredicateMethod）       | 返回对输入集合中的任何元素调用指定谓词方法的结果是否为 true。                                                                                                                                                         |
| .First （\[PredicateMethod\]） | 返回集合中的第一个元素。 如果传递了可选谓词，则将返回集合中对谓词的调用返回 true 的第一个元素。                                                                                                |
| .Last （\[PredicateMethod\]）  | 返回集合中的最后一个元素。 如果传递了可选谓词，则将返回集合中的最后一个元素，对该谓词的调用将返回 true。                                                                                                  |
| Min （\[KeyProjectorMethod\]）    | 返回集合中的最小元素。 可以指定一个可选的投影仪方法，以便在将每个方法与其他方法进行比较之前将其投影。                                                                                                                         |
| Max （\[KeyProjectorMethod\]）    | 返回集合中的最大元素。 可以指定一个可选的投影仪方法，以便在将每个方法与其他方法进行比较之前将其投影。                                                                                                                         |
| Single （\[PredicateMethod\]）    | 返回列表中的唯一元素（如果集合包含多个元素，则返回错误）。 如果指定了谓词，则将返回满足该谓词的单个元素（如果有多个元素满足该谓词，则函数将改为返回错误）。 |



**参数的签名**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">KeyProjectorMethod：（obj =&gt; 任意密钥）</td>
<td align="left">获取集合的对象并从该对象返回一个键。</td>
</tr>
<tr class="even">
<td align="left">KeyComparatorMethod：（（a，b） =&gt; 整数值）</td>
<td align="left">采用两个键并比较它们返回的内容：
<p>如果为（a &lt; b），则为-1</p>
<p>如果为0（a = = b）</p>
<p>如果为（a &gt; b），则为1</p></td>
</tr>
<tr class="odd">
<td align="left">PredicateMethod：（obj =&gt; 布尔值）</td>
<td align="left">获取集合的对象，并根据该对象是否满足某些条件，返回 true 或 false。</td>
</tr>
</tbody>
</table>



## <a name="supported-linq-syntax---string-manipulation"></a>支持的 LINQ 语法-字符串操作

所有字符串对象都有投影到它们中的以下方法，以便它们可供使用：

查询相关方法 & 属性

|                                     |                                                                                                                                                                                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .Contains （OtherString）           | 返回一个布尔值，该值指示输入字符串是否包含 OtherString。                                                                                                                                                 |
| .EndsWith （OtherString）           | 返回一个布尔值，该值指示输入字符串是否以 OtherString 结尾。                                                                                                                                                |
| 长度                              | 一个属性，该属性返回字符串的长度。                                                                                                                                                                                |
| .StartsWith （OtherString）         | 返回一个布尔值，该值指示输入字符串是否以 OtherString 开头。                                                                                                                                              |
| .Substring （StartPos，\[长度\]） | 从给定的起始位置开始，返回输入字符串中的子字符串。 如果提供了可选长度，则返回的子字符串将为指定的长度;否则，将会跳到字符串的末尾。 |



其他方法

|                              |                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------|
| .IndexOf （OtherString）     | 返回 OtherString 在输入字符串中的第一个匹配项的索引。 |
| .LastIndexOf （OtherString） | 返回 OtherString 在输入字符串中的最后一个匹配项的索引。  |



格式设置方法

|                                          |                                                                                                                                                                                                                                                     |
|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .PadLeft （TotalWidth）                  | 根据需要在字符串左侧添加空格，以便将字符串的总长度显示为指定的宽度。                                                                                                                    |
| .PadRight （TotalWidth）                 | 根据需要在字符串的右侧添加空格，以便将字符串的总长度显示为指定的宽度。                                                                                                                   |
| .Remove （StartPos，\[长度\]）         | 从输入字符串中删除以指定的起始位置开始的字符。 如果提供了可选长度参数，则将删除该字符的数量;否则为-将删除字符串末尾的所有字符。 |
| .Replace （SearchString，ReplaceString） | 用指定的 ReplaceString 替换输入字符串中的每个出现的 SearchString。                                                                                                                                                 |



字符串对象投影

除了直接投影到字符串对象的方法之外，任何本身具有字符串转换的对象都具有以下方法，并将其投影到该方法，使其可供使用：

|                      |                                                                                                                                                                                                                  |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .ToDisplayString ( ) | 返回对象的字符串转换。 这是将在对象的 dx 调用中显示的字符串转换。 可以提供格式设置说明符来设置 ToDisplayString 的输出格式。 |



下面的示例演示如何使用格式说明符。

```dbgcmd
kd> dx (10).ToDisplayString("d")
(10).ToDisplayString("d") : 10

kd> dx (10).ToDisplayString("x")
(10).ToDisplayString("x") : 0xa

kd> dx (10).ToDisplayString("o")
(10).ToDisplayString("o") : 012

kd> dx (10).ToDisplayString("b") 
(10).ToDisplayString("b")  : 0y1010
```

## <a name="span-iddebugging_plug_and_playspanspan-iddebugging_plug_and_playspanspan-iddebugging_plug_and_playspandebugging-plug-and-play-example"></a><span id="Debugging_Plug_and_Play"></span><span id="debugging_plug_and_play"></span><span id="DEBUGGING_PLUG_AND_PLAY"></span>调试即插即用示例


本部分说明如何使用与 LINQ 查询一起使用的内置调试器对象来调试即插即用对象。

**查看所有设备**

使用设备树上的 "*平展*" 查看所有设备。 

```dbgcmd
 1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
    [0x5]            : ROOT\spaceport\0000 (spaceport)
    [0x6]            : ROOT\KDNIC\0000 (kdnic)
    [0x7]            : ROOT\UMBUS\0000 (umbus)
    [0x8]            : ROOT\ACPI_HAL\0000
...
```

**网格显示**

与其他 dx 命令一样，你可以在命令执行之后右键单击该命令，然后单击 "显示为网格" 或将 "-g" 添加到命令以获取结果的网格视图。

```dbgcmd
# 0: kd> dx -g @$cursession.Devices.DeviceTree.Flatten(n => n.Children)
=====================================================================================================================================================================================================================================================================================================================
# =                                                              = (+) DeviceNodeObject = InstancePath                                                 = ServiceName               = (+) PhysicalDeviceObject                                    = State                          = (+) Resoures = (+) Children       =
=====================================================================================================================================================================================================================================================================================================================
= [0x0] : HTREE\ROOT\0                                         - {...}                - HTREE\ROOT\0                                                 -                           - 0xffffb6075614be40 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
= [0x1] : ROOT\volmgr\0000 (volmgr)                            - {...}                - ROOT\volmgr\0000                                             - volmgr                    - 0xffffb607561fbe40 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
= [0x2] : ROOT\BasicDisplay\0000 (BasicDisplay)                - {...}                - ROOT\BasicDisplay\0000                                       - BasicDisplay              - 0xffffb607560739b0 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
= [0x3] : ROOT\CompositeBus\0000 (CompositeBus)                - {...}                - ROOT\CompositeBus\0000                                       - CompositeBus              - 0xffffb607561f9060 : Device for "\Driver\PnpManager"        - DeviceNodeStarted (776)        - {...}        - [object Object]    =
...
```

**按状态查看设备**

使用*Where*指定特定设备状态。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State <operator> <state number>)
```

例如，若要查看处于状态 DeviceNodeStarted 的设备，请使用此命令。

```dbgcmd
1: kd>  dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State == 776)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State == 776)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
...
```

**查看未启动的设备**

使用此命令查看不处于状态 DeviceNodeStarted 的设备。

```dbgcmd
1: kd>  dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State != 776)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State != 776)                
    [0x0]            : ACPI\PNP0C01\1
    [0x1]            : ACPI\PNP0000\4&215d0f95&0
    [0x2]            : ACPI\PNP0200\4&215d0f95&0
    [0x3]            : ACPI\PNP0100\4&215d0f95&0
    [0x4]            : ACPI\PNP0800\4&215d0f95&0
    [0x5]            : ACPI\PNP0C04\4&215d0f95&0
    [0x6]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
    [0x7]            : ACPI\PNP0C02\1
    [0x8]            : ACPI\PNP0C02\2
```

**按问题代码查看设备**

使用*DeviceNodeObject*对象来查看具有特定问题代码的设备。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem <operator> <problemCode>)
```

例如，若要查看具有非零问题代码的设备，请使用此命令。 这会向 "[ **！ devnode**](-devnode.md) 0 21" 提供类似的信息。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**查看所有设备，无问题**

使用此命令可查看所有设备，但不会出现问题

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)                
    [0x0]            : ROOT\volmgr\0000 (volmgr)
    [0x1]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x2]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x3]            : ROOT\vdrvroot\0000 (vdrvroot)
...
```

**查看具有特定问题的所有设备**

使用此命令查看问题状态为0x16 的设备。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**按功能驱动程序查看设备**

使用此命令可以按功能驱动程序查看设备。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName <operator> <service name>)
```

若要使用特定功能驱动程序（如 atapi）查看设备，请使用此命令。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")                
    [0x0]            : PCIIDE\IDEChannel\4&10bf2f88&0&0 (atapi)
    [0x1]            : PCIIDE\IDEChannel\4&10bf2f88&0&1 (atapi)
```

**查看启动启动驱动程序的列表**

若要查看作为启动启动驱动程序加载的 winload.exe 的列表，你需要位于具有 LoaderBlock 访问权限的上下文中，并且仍有足够的 LoaderBlock。 例如，在 nt 期间IopInitializeBootDrivers. 断点可以设置为在此上下文中停止。

```dbgcmd
1: kd> g
Breakpoint 0 hit
nt!IopInitializeBootDrivers:
8225c634 8bff            mov     edi,edi
```

使用 "？" 命令来显示启动驱动程序结构。

```dbgcmd
1: kd> ?? LoaderBlock->BootDriverListHead
struct _LIST_ENTRY
 [ 0x808c9960 - 0x808c8728 ]
   +0x000 Flink            : 0x808c9960 _LIST_ENTRY [ 0x808c93e8 - 0x808a2e18 ]
   +0x004 Blink            : 0x808c8728 _LIST_ENTRY [ 0x808a2e18 - 0x808c8de0 ]
```

使用 FromListEntry 调试器对象来查看数据，并使用 nt 的起始地址进行查看！\_列表\_条目结构。

```dbgcmd
1: kd> dx Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")
Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")                
    [0x0]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x1]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x2]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x3]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x4]            [Type: _BOOT_DRIVER_LIST_ENTRY]
    [0x5]            [Type: _BOOT_DRIVER_LIST_ENTRY]
...
```

使用-g 选项创建数据的网格视图。

```dbgcmd
dx -r1 -g Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")
```

**按功能查看设备**

使用 DeviceNodeObject. CapabilityFlags 对象按功能查看设备。

```dbgcmd
dx -r1 @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => (n.DeviceNodeObject.CapabilityFlags & <flag>) != 0)
```

此表总结了使用常见设备功能标志的 dx 命令的用法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">去除</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x10) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x10) != 0)                
    [0x0]            : SWD\PRINTENUM\{2F8DBBB6-F246-4D84-BB1D-AA8761353885}
    [0x1]            : SWD\PRINTENUM\{F210BC77-55A1-4FCA-AA80-013E2B408378}
    [0x2]            : SWD\PRINTENUM\{07940A8E-11F4-46C3-B714-7FF9B87738F8}
    [0x3]            : DISPLAY\Default_Monitor\6&1a097cd8&0&UID5527112 (monitor)</code>

</div></td>
</tr>
<tr class="even">
<td align="left">UniqueID</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x40) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x40) != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\spaceport\0000 (spaceport)
...</code>

</div></td>
</tr>
<tr class="odd">
<td align="left">SilentInstall</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x80) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x80) != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\spaceport\0000 (spaceport)
...</code>

</div></td>
</tr>
<tr class="even">
<td align="left">RawDeviceOk</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x100) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x100) != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : SWD\MMDEVAPI\MicrosoftGSWavetableSynth
    [0x2]            : SWD\IP_TUNNEL_VBUS\IP_TUNNEL_DEVICE_ROOT
...</code>

</div></td>
</tr>
<tr class="odd">
<td align="left">SurpriseRemovalOK</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x200) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags & 0x200) != 0)                
    [0x0]            : SWD\MMDEVAPI\MicrosoftGSWavetableSynth
    [0x1]            : SWD\IP_TUNNEL_VBUS\IP_TUNNEL_DEVICE_ROOT
    [0x2]            : SWD\PRINTENUM\PrintQueues
...</code>

</div></td>
</tr>
</tbody>
</table>


有关 CapabilityFlags 的详细信息，请参阅[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)。


## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md) 

---







