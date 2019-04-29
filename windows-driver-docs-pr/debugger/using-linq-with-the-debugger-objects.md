---
title: 将 LINQ 与调试器对象配合使用
description: 使用 LINQ 与调试器对象。 可以使用调试器对象使用 LINQ 语法，用于搜索和操作数据。
keywords:
- 将 LINQ 与调试器对象配合使用
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: e3cbc22e4063fc75bd6358e6363d1f346243e78d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390538"
---
# <a name="using-linq-with-the-debugger-objects"></a>将 LINQ 与调试器对象配合使用

可以使用调试器对象使用 LINQ 语法，用于搜索和操作数据。 使用 LINQ 语法使用 dx 命令可以使用调试器命令相比更一致的体验。 无论你正在查看哪个调试器对象一致的输出和选项。 LINQ 查询允许您提出问题如"什么是正在运行的大多数线程前 5 个进程？"。

调试器对象被投影到一个命名空间根节点的"调试器"。 进程、 模块、 线程、 堆栈、 堆栈帧和本地变量都可用于 LINQ 查询。

LINQ 是从概念上讲类似到结构化查询语言 (SQL)，用于查询数据库。 许多 LINQ 方法可用于搜索、 筛选和分析调试数据。 LINQC#使用方法语法。 LINQ 和 LINQ 的详细信息的C#语法，请参阅[中的 LINQ 入门C#](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/getting-started-with-linq)

使用中的调试器支持的 LINQ 使用 LINQ 的"方法语法"，并不是"查询语法"。 您可以找到有关之间的区别的更多详细信息[LINQ （语言集成查询）](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)。

如下所示的 LINQ 命令可以在调试器对象。 所有。任何。计数。首先。平展。GroupBy。最后。OrderBy。OrderByDescending。选择、 和。在何处。 这些方法便遵循 （尽可能） C# LINQ 方法窗体。

## <a name="native-debugger-objects"></a>本机调试器对象

本机调试器对象表示各种构造和调试器环境的行为。 如调试器对象包括以下内容。

- 会议
- 线程 / 线程
- 进程数 / 处理
- 堆栈帧 / 堆栈帧
- 本地变量
- 模块 / 模块
- 实用程序
- 状态
- 设置

此外可以使用与 NatVis 调试器对象。 有关详细信息请参阅[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)。 与 JavaScript 一起使用调试器对象的信息，请参阅[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。 有关使用C++和驱动程序对象，请参阅[调试器数据模型C++概述](data-model-cpp-overview.md)。

## <a name="dx-command"></a>Dx 命令

示例如下所示使用 dx 命令，使用 dx 命令中，有关详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

## <a name="developing-a-linq-query"></a>开发 LINQ 查询

开发 LINQ 调试器对象查询的一种方法是使用将显示，以浏览数据模型，以首先找到将使用的调试器对象在查询中的 DML 链接。

对于此示例中，我们想要显示的进程的列表中的内核调试会话和线程数为每个这些进程。

若要开始我们的探索我们可以使用 dx 命令显示顶部级别调试器对象。

```dbgcmd
0: kd> dx Debugger
Debugger
    Sessions
    Settings
    State
    Utility
```

单击后的最高级别主题，我们确定，因此我们单击以显示它包含的 DML 链接的外观最有趣的是，会话*进程*。 

```dbgcmd
0: kd> dx -r1 Debugger.Sessions[0]
Debugger.Sessions[0]                 : Remote KD: KdSrv:Server=@{<Local>},Trans=@{NET:Port=50005,Key=MyKey}
    Processes
    Id               : 0
    Attributes
```

然后我们单击进一步向下查看特定进程和我们看到*线程*与关联进程都可用。 当我们单击*线程*进程之一，我们查看与该进程关联的线程的所有可用。


```dbgcmd
0: kd> dx -r1 Debugger.Sessions[0].Processes[1428].Threads
Debugger.Sessions[0].Processes[1428].Threads
    [0x598]          : <Unable to get stack trace> [Switch To]
    [0x1220]         : <Unable to get stack trace> [Switch To]
    [0x6f8]          : nt!KiSwapContext+0x76 (fffff806`4466a186)  [Switch To]
    [0x128c]         : <Unable to get stack trace> [Switch To]
    [0x27e4]         : nt!KiSwapContext+0x76 (fffff806`4466a186)  [Switch To] 
```

现在，我们知道，我们需要显示与进程关联的线程数的数据是在调试器对象模型中可用。

若要使 LINQ 查询稍有较短，我们可以使用[系统定义的变量](#system-defined-variables)以显示与当前会话相关联的过程本主题后面所述。

```dbgcmd
0: kd> dx @$cursession.Processes
@$cursession.Processes                
    [0x0]            : Idle [Switch To]
    [0x4]            : System [Switch To]
    [0x90]           : Registry [Switch To]
...
```

接下来添加 select 语句。 开始时，我们可以指定名称字段。

```dbgcmd
0: kd> dx @$cursession.Processes.Select(p => p.Name)
@$cursession.Processes.Select(p => p.Name)                
    [0x0]            : Idle
    [0x4]            : System
    [0x90]           : Registry
...
```

对于我们的方案，我们还需要线程的数。 由于有两个字段，创建匿名类型使用*新*，类似于C#的匿名类型语法如下所述中[用户定义的变量](#user-defined-variables)。

```dbgcmd
dx @$cursession.Processes.Select(p => new {Name = p.Name, Threads = p.Threads})
```

使用该命令时，dx 不实际打印出的名称不再，因此添加-r2 （recurse 两个级别），以显示名称和线程。

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

现在我们要显示的进程名称和主题的列表。 若要显示 ThreadCount，请使用 *。Count （)* 方法。


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

若要查看哪些进程拥有大量的线程，对列表排序时使用线程计数*OrderByDescending*。

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

 若要格式化的网格更改中呈现-r2 是-g。 不需级别的递归不指定，因为网格选项会相应地显示的列。 最后，添加，d 格式说明符，以输出十进制值。

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

此示例显示了正在运行的大多数线程前 5 个进程：

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

此示例显示在插设备树中按物理设备对象的驱动程序的名称分组的设备。 并非所有输出会显示。

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

## <a name="dx-command-tab-auto-completion"></a>Dx 命令 tab 键自动完成功能

上下文选项卡键自动完成已意识的 LINQ 查询方法，并将适用于 lambda 参数。

例如，键入 （或复制并粘贴） 到调试器的以下文本。 然后按 TAB 键多次遍历潜在完成。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.
```

按 TAB 键，直到"。显示名称"。 添加右括号")"，然后按 enter 以执行该命令。

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

此示例演示使用键比较器的方法完成。 替换将显示字符串方法，因为该密钥是一个字符串。

```dbgcmd
dx -r2 Debugger.Sessions.First().Processes.Select(p => new {Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.Name, (a, b) => a.
```

按 TAB 键，直到"。长度"会显示。 添加右括号")"，然后按 enter 以执行该命令。

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

可以通过使用 @$ 在变量名称来定义的用户定义变量。 用户定义变量可以 lambda 的 LINQ 查询等结果分配给任何 dx 可以利用，例如。

可以创建和设置此类用户变量的值。

```dbgcmd
kd> dx @$String1="Test String"
```

可以显示使用定义的用户变量*Debugger.State.UserVariables*或 *@$ vars*。

```dbgcmd
kd> dx Debugger.State.UserVariables
Debugger.State.UserVariables : 
    mySessionVar     : 
    String1          : Test String
```

您可以删除变量的使用。删除。

```dbgcmd
kd> dx @$vars.Remove("String1")
```

此示例演示如何引用 Debugger.Sesssions 定义的用户变量。

```dbgcmd
kd> dx @$mySessionVar = Debugger.Sessions
```

如下所示，然后可以使用用户定义变量。

```dbgcmd
kd> dx -r2 @$mySessionVar 
@$mySessionVar   : 
    [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{COM:Port=\\.\com3,Baud=115200,Timeout=4000}
        Processes        : 
        Devices     
```
## <a name="system-defined-variables"></a>系统定义的变量

可以在任何 LINQ dx 查询中使用以下系统定义变量。

-   @$ cursession-当前会话

-   @$ curprocess-当前进程

-   @$ curthread-当前线程

此示例演示使用系统定义的变量。

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

## <a name="user-defined-variables---anonymous-types"></a>用户定义的变量的匿名类型

完成此创建动态对象使用C#匿名类型语法 （新 {...}）。 有关更多信息，请参见有关匿名类型，请参阅[匿名类型 (C#编程指南)](https://msdn.microsoft.com/library/bb397696.aspx)。 本示例创建一个匿名类型包含整数和字符串值。

```dbgcmd
kd> dx -r1 new { MyInt = 42, MyString = "Hello World" }
new { MyInt = 42, MyString = "Hello World" } : 
    MyInt            : 42
    MyString         : Hello World
```


## <a name="function-objects-lambda-expressions"></a>函数对象 （Lambda 表达式）

许多用于查询数据的方法都基于重复运行用户提供跨集合中的对象的函数的概念。 若要支持查询和操作调试器中的数据的能力，dx 命令支持使用等效的 lambda 表达式C#语法。 Lambda 表达式定义的使用情况 =&gt;运算符，如下所示：

（参数） =&gt; （结果）

若要查看如何将 LINQ 用于 dx，请尝试此简单示例 5 和 7 一起添加。

```dbgcmd
kd> dx ((x, y) => (x + y))(5, 7) 
```

Dx 命令回显返回 lambda 表达式，并显示结果 12。

```dbgcmd
((x, y) => (x + y))(5, 7)  : 12
```

此示例中 lambda 表达式将字符串"Hello"和"World"。

```dbgcmd
kd> dx ((x, y) => (x + y))("Hello", "World")
((x, y) => (x + y))("Hello", "World") : HelloWorld
```


## <a name="supported-linq-syntax---query-methods"></a>支持 LINQ 语法的查询方法

哪些 dx 定义为可迭代的任何对象 （是的本机数组，它具有 NatVis 编写描述为一个容器或调试器扩展对象的类型） 具有投影到其上的一系列 LINQ （或等效的 LINQ） 方法。 这些查询方法如下所述。 所有的查询方法之后列出了查询方法的参数的签名。

筛选方法

|                            |                                                                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| .其中 (PredicateMethod) | 返回一个新集合包含谓词的方法为其返回 true 的输入集合中的每个对象的对象。 |



投影方法

|                                     |                                                                                                                                                                                                                                                                                                                             |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .平展 ( \[KeyProjectorMethod\] ) | 采用一个输入的容器的容器 （树），并平展到单个容器中具有在树中的每个元素。 如果提供的可选密钥投影仪方法，则树被视为其自身的容器和这些密钥由对投影方法的调用是键的容器。 |
| .选择 (KeyProjectorMethod)      | 返回包含结果的输入集合中每个对象调用投影仪方法的对象的新集合。                                                                                                                                                                                          |



分组方法

|                                                                                                                            |                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .GroupBy (KeyProjectorMethod， \[KeyComparatorMethod\] )                                                                   | 返回通过将分组具有与确定相同的密钥通过调用关键投影仪方法的输入集合中的所有对象的新集合的集合。 可以提供可选的比较运算符方法。 |
| 联接 (InnerCollection，外部键选择器方法、 内部键选择器方法，结果选择器方法\[ComparatorMethod\]) | 联接两个序列基于的键选择器函数，并提取值对。 此外可以指定可选的比较运算符方法。                                                                        |
| Intersect (InnerCollection， \[ComparatorMethod\])                                                                          | 返回交集，这意味着在每个两个集合中出现的元素。 此外可以指定可选的比较运算符方法。                                                               |
| Union (InnerCollection， \[ComparatorMethod\])                                                                              | 返回并集，这意味着出现在两个集合的唯一元素。 此外可以指定可选的比较运算符方法。                                                             |



数据集的方法

|                                                |                                                                                                                                                                                                   |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 包含 (对象， \[ComparatorMethod\])        | 确定序列是否包含指定的元素。 提供的将与序列中的条目比较元素每次调用它，可以是可选的比较运算符方法。 |
| 非重复 (\[ComparatorMethod\])                | 删除重复的集合中的值。 可以提供可选的比较运算符方法调用每个时间对象集合中必须进行比较。                                      |
| 除 (InnerCollection， \[ComparatorMethod\]) | 返回差集，这意味着第二个集合中不会出现一个集合的元素。 可以指定可选的比较运算符方法。                                 |
| Concat (InnerCollection)                       | 连接两个序列以组成一个序列。                                                                                                                                                  |



排序方法

|                                                                    |                                                                                                                                                                                                      |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .OrderBy (KeyProjectorMethod， \[KeyComparatorMethod\] )           | 提供的输入集合中每个对象调用密钥投影方法升序顺序根据某个键集合进行排序。 可以提供可选的比较运算符方法。  |
| .OrderByDescending (KeyProjectorMethod， \[KeyComparatorMethod\] ) | 提供的输入集合中每个对象调用密钥投影方法降序根据某个键的顺序集合进行排序。 可以提供可选的比较运算符方法。 |



聚合方法

|                            |                                                                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| Count （)                   | 集合中返回的元素数的方法。                                                                                |
| Sum (\[ProjectionMethod\]) | 计算集合中值的总和。 可以选择指定总和发生之前转换元素的投影仪方法。 |



Skip 方法

|                             |                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| 跳过 （计数）                | 跳过序列中的指定位置之前的元素。                                      |
| SkipWhile (PredicateMethod) | 跳过基于谓词函数，直到元素不符合条件的元素。 |



执行方法

|                             |                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| 采用 （计数）                | 获取序列中的指定位置之前的元素。                                      |
| TakeWhile (PredicateMethod) | 获取基于谓词函数，直到元素不符合条件的元素。 |



比较方法

|                                                       |                                                                                                                                  |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| SequenceEqual (InnerCollection， \[ComparatorMethod\]) | 确定两个序列是否通过以成对方式比较元素相等。 可以指定可选的比较运算符。 |



错误处理方法

|                                     |                                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------|
| AllNonError (PredicateMethod)       | 返回集合中的所有非错误元素是否都满足给定的条件。 |
| FirstNonError (\[PredicateMethod\]) | 返回一个集合，其中并不是错误的第一个元素。                    |
| LastNonError (\[PredicateMethod\])  | 返回一个集合，其中并不是错误的最后一个元素。                     |



其他方法

|                                |                                                                                                                                                                                                                                                                              |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .所有 (PredicateMethod)       | 返回在输入集合中的每个元素调用指定的谓词方法的结果是否为 true。                                                                                                                                                       |
| .任何 (PredicateMethod)       | 返回在输入集合中任何元素上调用指定的谓词方法的结果是否为 true。                                                                                                                                                         |
| .第一个 ( \[PredicateMethod\] ) | 返回集合中的第一个元素。 如果传递的可选谓词，则在调用该谓词为其返回 true 的集合中返回的第一个元素。                                                                                                |
| .最后一个 ( \[PredicateMethod\] )  | 返回集合中的最后一个元素。 如果传递的可选谓词，则在调用该谓词为其返回 true 的集合中返回的最后一个元素。                                                                                                  |
| 最小值 (\[KeyProjectorMethod\])    | 返回集合的最小元素。 可以指定可选的投影仪方法以之前它与其他项目的每个方法。                                                                                                                         |
| 最大值 (\[KeyProjectorMethod\])    | 返回集合的最大元素。 可以指定可选的投影仪方法以之前它与其他项目的每个方法。                                                                                                                         |
| 单个 (\[PredicateMethod\])    | 从列表 （或如果集合包含多个元素出现错误） 返回的唯一元素。 如果指定了一个谓词，将返回满足该谓词的单个元素 （如果多个元素满足它，则函数返回错误相反）。 |



**参数的签名**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">KeyProjectorMethod: (obj =&gt;任意键)</td>
<td align="left">接收集合的对象并从该对象返回一个键。</td>
</tr>
<tr class="even">
<td align="left">KeyComparatorMethod: ((a，b) =&gt;整数值)</td>
<td align="left">采用两个密钥并将其比较返回：
<p>-1，如果 ( &lt; b）。</p>
<p>0 (= = b）。</p>
<p>1，如果 ( &gt; b）。</p></td>
</tr>
<tr class="odd">
<td align="left">PredicateMethod: (obj =&gt;布尔值)</td>
<td align="left">接收集合的对象并返回 true 或 false 基于该对象是否符合特定的准则。</td>
</tr>
</tbody>
</table>



## <a name="supported-linq-syntax---string-manipulation"></a>支持的 LINQ 语法的字符串操作

字符串的所有对象都具有以下方法投影到它们，以便它们可供使用：

查询相关方法和属性

|                                     |                                                                                                                                                                                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .包含 (OtherString)           | 返回一个布尔值，该值指示输入的字符串是否包含 OtherString。                                                                                                                                                 |
| .EndsWith (OtherString)           | 返回一个布尔值，该值指示输入的字符串是否以 OtherString 结束。                                                                                                                                                |
| 长度                              | 属性返回字符串的长度。                                                                                                                                                                                |
| .StartsWith (OtherString)         | 返回一个布尔值，该值指示输入的字符串是否以 OtherString 开头。                                                                                                                                              |
| .子字符串 (正好从，\[长度\]) | 返回在给定的开始位置开始的输入字符串中的子字符串。 如果未提供可选的长度，则返回的子字符串将为指定的长度;否则 – 它将转到字符串的末尾。 |



杂项方法

|                              |                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------|
| .IndexOf ( OtherString )     | 返回的第一个匹配项 OtherString 输入字符串内的索引。 |
| .LastIndexOf ( OtherString ) | 返回的最后一个匹配项的 OtherString 输入字符串内的索引。  |



格式设置方法

|                                          |                                                                                                                                                                                                                                                     |
|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .PadLeft ( TotalWidth )                  | 以将字符串的总长度到指定的宽度根据字符串的左侧和右侧添加空格。                                                                                                                    |
| .PadRight (TotalWidth)                 | 根据字符串的右侧添加空格，以将字符串的总长度到指定的宽度。                                                                                                                   |
| .删除 (正好从，\[长度\])         | 从输入字符串为指定的起始位置开始删除字符。 如果提供可选的长度参数，则将删除该数目的字符;否则 – 到结尾的字符串的所有字符将被都删除。 |
| .Replace ( SearchString, ReplaceString ) | 替换指定 ReplaceString SearchString 在输入字符串中的每个匹配项。                                                                                                                                                 |



字符串对象投影

除了投影直接到字符串对象，任何对象上的方法本身有字符串转换中是否有投影到它，使其方法可以使用以下方法：

|                      |                                                                                                                                                                                                                  |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .ToDisplayString （) | 返回的对象的字符串转换。 这是将在 dx 调用对象中显示该字符串转换。 你可以提供可 ToDisplayString 输出格式设置的格式设置说明符。 |



下面的示例说明了使用格式说明符。

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

## <a name="span-iddebuggingplugandplayspanspan-iddebuggingplugandplayspanspan-iddebuggingplugandplayspandebugging-plug-and-play-example"></a><span id="Debugging_Plug_and_Play"></span><span id="debugging_plug_and_play"></span><span id="DEBUGGING_PLUG_AND_PLAY"></span>调试插示例


本部分演示了如何将内置的调试器对象与 LINQ 查询一起使用，可用于调试插对象。

**查看所有设备**

使用*Flatten*设备树以查看所有设备上。 

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

与其他 dx 命令，可以右键单击命令后执行该和单击"显示为网格"，或添加"-g"命令来获取结果的网格视图。

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

使用*其中*指定特定设备状态。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.State <operator> <state number>)
```

例如，若要查看处于状态 DeviceNodeStarted 设备使用此命令。

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

**视图未启动设备**

使用此命令来查看设备不处于状态 DeviceNodeStarted。

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

**通过故障代码，以查看设备**

使用*DeviceNodeObject.Problem*到具有特定问题的代码查看设备的对象。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem <operator> <problemCode>)
```

例如，若要查看设备具有非零故障代码，以使用此命令。 这提供了类似的信息为"[**！ devnode** ](-devnode.md) 0 21"。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem != 0)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**查看不会有问题的所有设备**

使用此命令以查看不会有问题的所有设备

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0)                
    [0x0]            : ROOT\volmgr\0000 (volmgr)
    [0x1]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x2]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x3]            : ROOT\vdrvroot\0000 (vdrvroot)
...
```

**查看与特定问题的所有设备**

使用此命令以查看具有 0x16 问题状态的设备。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.DeviceNodeObject.Problem == 0x16)                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ACPI\PNP0700\4&215d0f95&0 (fdc)
```

**查看设备驱动程序函数**

使用此命令来查看设备功能驱动程序。

```dbgcmd
dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName <operator> <service name>)
```

若要查看使用某些功能驱动程序，如 atapi，设备使用此命令。

```dbgcmd
1: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.ServiceName == "atapi")                
    [0x0]            : PCIIDE\IDEChannel\4&10bf2f88&0&0 (atapi)
    [0x1]            : PCIIDE\IDEChannel\4&10bf2f88&0&1 (atapi)
```

**查看启动开始驱动程序的列表**

若要查看哪些 winload 列表加载为启动开始驱动程序，您需要在其中可以访问 LoaderBlock，提前足够的上下文中 LoaderBlock 是仍周围。 例如，在为 nt ！IopInitializeBootDrivers。 可以设置断点以停止在此上下文中。

```dbgcmd
1: kd> g
Breakpoint 0 hit
nt!IopInitializeBootDrivers:
8225c634 8bff            mov     edi,edi
```

使用?? 若要显示的启动驱动程序结构的命令。

```dbgcmd
1: kd> ?? LoaderBlock->BootDriverListHead
struct _LIST_ENTRY
 [ 0x808c9960 - 0x808c8728 ]
   +0x000 Flink            : 0x808c9960 _LIST_ENTRY [ 0x808c93e8 - 0x808a2e18 ]
   +0x004 Blink            : 0x808c8728 _LIST_ENTRY [ 0x808a2e18 - 0x808c8de0 ]
```

Debugger.Utility.Collections.FromListEntry 调试器对象用于查看数据，使用 nt 的起始地址的 ！\_列表\_条目结构。

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

使用-g 选项创建的数据网格视图。

```dbgcmd
dx -r1 -g Debugger.Utility.Collections.FromListEntry(*(nt!_LIST_ENTRY *)0x808c9960, "nt!_BOOT_DRIVER_LIST_ENTRY", "Link")
```

**查看设备的功能**

通过使用 DeviceNodeObject.CapabilityFlags 对象的功能来查看设备。

```dbgcmd
dx -r1 @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => (n.DeviceNodeObject.CapabilityFlags & <flag>) != 0)
```

下表汇总了与常见设备功能标志 dx 命令的使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">可移动</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x10) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x10) != 0)                
    [0x0]            : SWD\PRINTENUM\{2F8DBBB6-F246-4D84-BB1D-AA8761353885}
    [0x1]            : SWD\PRINTENUM\{F210BC77-55A1-4FCA-AA80-013E2B408378}
    [0x2]            : SWD\PRINTENUM\{07940A8E-11F4-46C3-B714-7FF9B87738F8}
    [0x3]            : DISPLAY\Default_Monitor\6&amp;1a097cd8&amp;0&amp;UID5527112 (monitor)</code>

</div></td>
</tr>
<tr class="even">
<td align="left">UniqueID</td>
<td align="left"><div class="code">

<code>dbgcmd
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x40) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x40) != 0)                
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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x80) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x80) != 0)                
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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x100) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x100) != 0)                
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
0: kd&gt; dx -r1 @$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x200) != 0)
@$cursession.Devices.DeviceTree.Flatten(n =&gt; n.Children).Where(n =&gt; (n.DeviceNodeObject.CapabilityFlags &amp; 0x200) != 0)                
    [0x0]            : SWD\MMDEVAPI\MicrosoftGSWavetableSynth
    [0x1]            : SWD\IP_TUNNEL_VBUS\IP_TUNNEL_DEVICE_ROOT
    [0x2]            : SWD\PRINTENUM\PrintQueues
...</code>

</div></td>
</tr>
</tbody>
</table>


有关 CapabilityFlags 详细信息，请参阅[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)。


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)

[中 JavaScript 扩展本机调试器对象](native-objects-in-javascript-extensions.md) 

---







