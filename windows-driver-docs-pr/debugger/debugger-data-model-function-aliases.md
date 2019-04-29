---
title: 调试器数据模型函数别名
description: 函数别名是调试器的用户可以访问调试器扩展中定义的功能的快速唯一短名称。
keywords:
- 调试器数据模型函数别名
ms.date: 03/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: c04dcac55ffd45c03742252a279d6f1ed3a7bc69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368539"
---
# <a name="debugger-data-model-function-aliases"></a>调试器数据模型函数别名

函数别名是唯一的短名称调试器的用户可以访问调试器扩展中定义的功能 (编写的C++或 JavaScript 等一些脚本编写环境)。 此短名称获取与数据模型函数对象 （可实现 IModelMethod 对象） 相关联。 该函数采用任意数量的参数并返回单个值。 调用的函数别名并做了什么的效果的值依赖于如何调用函数别名和哪些主机调试器调用中。 

本主题假定读者熟悉的调试器对象模型和 JavaScript。 与 JavaScript 一起使用调试器对象的信息，请参阅[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

一些示例如下所示使用 dx 命令中的使用 dx 命令中，有关详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。 除了使用 LINQ 中所述[使用调试器对象与 LINQ](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects)。



## <a name="using-function-alias-as-extension-commands"></a>使用作为扩展命令别名的函数

可以调用在 WinDbg 预览版中创建的所有函数别名，就像调试扩展 **！** "身份"命令。 如果该函数不采用任何参数，只需调用 ！ aliasName 将导致要调用的函数以及要显示的结果值。 作为示例 （使用 JavaScript 扩展创建）

例如，此函数提供了两个常量值*pi*并*e*。

```cpp
function __constants()
{
    return { math_constants : { pi :  3.1415926535 , e :  2.7182818284}, description : "Archimedes' pi and Euler's number e" };
}

function initializeScript()
{
    return [new host.functionAlias(__constants, "constants")];
}
```

调用的函数别名的结果如下所示。 

```dbgcmd
0:000> !constants
@$constants()                 : [object Object]
    math_constants   : [object Object]
    description      : Archimedes' pi and Euler's number e
```

将自动生成 DML 链接到复杂的对象。 单击上面所示 math_constants 将产生以下输出。 

```dbgcmd
0:000> dx -r1 @$constants().math_constants
@$constants().math_constants                 : [object Object]
    pi               : 3.141593
    e                : 2.718282
```


如果函数具有参数，它们可以提供后函数别名命令本身。 请注意，在函数别名命令后出现的任何内容被视为一个表达式，这种情况下计算。 文本字符串不直接传递到函数。 对于单个自变量表达式，它可以来自后函数别名命令本身。 对于多个自变量，它们应该是用圆括号括起来，就好像函数调用下一个示例中所示。


```cpp
function __oneArgument(x)
{
    return -x;
}

function __twoArguments(x, y)
{
    return x + y;
}

function initializeScript()
{
    return [new host.functionAlias(__oneArgument, "neg"),
            new host.functionAlias(__twoArguments, "add")];
}
```

可以调用这两个函数，如下所示。

```dbgcmd
0:000> !neg 42
@$neg(42)        : -42

0:000> !add (5, 7)
@$add(5, 7)      : 0xc
```


## <a name="function-alias-use-with-the-dx-expression-evaluator"></a>函数别名与 dx 表达式计算器，请使用

除了调试扩展 **！** "身份"命令调用别名函数的语法，所有与函数别名关联的名称都直接提供 dx 表达式计算器时加*@$* 如下所示。  

```dbgcmd
0:000> dx @$neg(42)
@$neg(42)        : -42

0:000> dx @$add(99, 77)
@$add(99, 77)    : 0xb0
```


## <a name="function-alias-design-considerations"></a>函数别名设计注意事项

函数别名永远不应在绝大部分数据中的哪些功能公开模型扩展的唯一方式。 数据模型扩展 (比如在C++或 JavaScript) 应几乎始终包括它所公开的类型或其他调试程序的概念与关联的数据。 与进程相关联的所有操作应都是 Debugger.Models.Process 或该对象的一个子命名空间下。 函数别名可在方便的入门到 （或转换） 可能需要相当长的时间的查询的数据。 

作为内核模式示例中，以下查询将即插即用设备树，并平展到一个简单的设备的平面列表： 

```dbgcmd
0: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children),5
@$cursession.Devices.DeviceTree.Flatten(n => n.Children),5                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
    [...]     
```

此 JavaScript 代码演示如何可以实现此作为函数别名。 

```dbgcmd
function __flatDevices()
{
    return host.currentSession.Devices.DeviceTree.Flatten(n => n.Children);
}

function initializeScript()
{
    return [new host.functionAlias(__flatDevices, "devices")];
}
```

然后可以作为调试扩展命令调用的函数别名。 

```dbgcmd
0: kd> !devices
@$devices()                
    [0x0]            : HTREE\ROOT\0
    [0x1]            : ROOT\volmgr\0000 (volmgr)
    [0x2]            : ROOT\BasicDisplay\0000 (BasicDisplay)
    [0x3]            : ROOT\CompositeBus\0000 (CompositeBus)
    [0x4]            : ROOT\vdrvroot\0000 (vdrvroot)
    [0x5]            : ROOT\spaceport\0000 (spaceport)

    ...
```

使用函数别名的优势之一是，它可以是进一步优化使用 dx 语法。 在此示例中，where 子句添加要查找的设备节点，包含"硬盘"。

```dbgcmd
0: kd> dx @$devices().Where(n => n.InstancePath.Contains("Harddisk"))
@$devices().Where(n => n.InstancePath.Contains("Harddisk"))                
    [0x0]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot1
    [0x1]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot2
    [0x2]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot3
    [0x3]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot4
    [0x4]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot5
    [0x5]            : STORAGE\VolumeSnapshot\HarddiskVolumeSnapshot6
```


使用功能的别名-，可以使用如下所示的 LINQ 命令。所有。任何。计数。首先。平展。GroupBy。最后。OrderBy。OrderByDescending。选择、 和。在何处。 这些方法便遵循 （尽可能） C# LINQ 方法窗体。 有关详细信息请参阅[使用调试器对象与 LINQ](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects)。



**网格显示**

与其他 dx 命令，可以右键单击命令后执行该和单击"显示为网格"，或添加"-g"命令来获取结果的网格视图。 然后可以单击任何列进行排序，例如 InstancePath 上。

```dbgcmd
0: kd> dx -g @$devices().OrderBy(obj => obj.@"InstancePath")
```

![函数别名网格排序的输出显示行调试器对象。](images/debugger-objects-function-alias.png) 



## <a name="process-threads-example"></a>进程线程示例

调试器对象被投影到一个命名空间根节点的"调试器"。 进程、 模块、 线程、 堆栈、 堆栈帧和本地变量都可用于 LINQ 查询。

JavaScript 此示例演示如何显示当前会话的进程的线程计数：

```dbgcmd
function __Processes()
{
    return host.currentSession.Processes.Select(p => ({Name: p.Name, ThreadCount: p.Threads.Count()}));
}

function initializeScript()
{
    return [new host.functionAlias(__Processes, "Processes")];
}
```
这将显示的示例将输出与 ！进程函数别名。


```dbgcmd
0: kd> !Processes
@$Processes()                
    [0x0]            : [object Object]
    [0x4]            : [object Object]
    [0x1b4]          : [object Object]
    [0x248]          : [object Object]
    [0x2c4]          : [object Object]
    [0x340]          : [object Object]
    [0x350]          : [object Object]
    [0x3d4]          : [object Object]
    [0x3e8]          : [object Object]
    [0x4c]           : [object Object]
    [0x214]          : [object Object]
    [0x41c]          : [object Object]
    [0x494]          : [object Object]

...    
```
显示在此示例中具有最大线程数的前 5 个进程。

```dbgcmd
0: kd> dx -r1 @$Processes().OrderByDescending(p =>p.ThreadCount),5
@$Processes().OrderByDescending(p =>p.ThreadCount),5                
    [0x4]            : [object Object]
    [0x180]          : [object Object]
    [0x978]          : [object Object]
    [0xda4]          : [object Object]
    [0x3e8]          : [object Object]
    [...]   
```



## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[使用 LINQ 与调试器对象](using-linq-with-the-debugger-objects.md)

[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)

[中 JavaScript 扩展本机调试器对象](native-objects-in-javascript-extensions.md) 

---






