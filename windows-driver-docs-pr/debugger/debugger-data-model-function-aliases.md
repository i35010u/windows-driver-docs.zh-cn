---
title: 调试器数据模型函数别名
description: 函数别名是一个快速唯一的短名称，调试器的用户可以在其中访问调试器扩展中定义的功能。
keywords:
- 调试器数据模型函数别名
ms.date: 03/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 372ce2f9383dd837a4169206eb2f2f35d34b958c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211203"
---
# <a name="debugger-data-model-function-aliases"></a>调试器数据模型函数别名

函数别名是一个唯一的短名称，通过该名称，调试器的用户可以访问调试器扩展中定义的功能， (是使用 c + + 编写的还是某些脚本环境（如 JavaScript) ）。 此短名称与 (实现 IModelMethod) 的对象的数据模型函数对象相关联。 该函数采用任意数量的参数，并返回单个值。 调用函数别名以及使用该值完成的效果取决于调用函数别名的方式，以及在其中调用函数别名的宿主调试器。 

本主题假定读者熟悉调试器对象模型和 JavaScript。 有关将调试器对象与 JavaScript 一起使用的信息，请参阅 [Javascript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

此处显示的一些示例使用 dx 命令，有关使用 dx 命令的详细信息，请参阅 [dx (显示调试器对象模型表达式) ](dx--display-visualizer-variables-.md)。 此外，还使用了 LINQ，其中介绍了如何将 [Linq 与调试器对象结合使用](./using-linq-with-the-debugger-objects.md)。



## <a name="using-function-alias-as-extension-commands"></a>使用函数别名作为扩展命令

在 WinDbg Preview 中创建的所有函数别名都可以调用，就像它们是调试扩展 **！** "感叹号" 命令。 如果函数不采用参数，只需调用！ aliasName 将导致调用函数并显示结果值。  (使用 JavaScript 扩展性创建的示例) 

例如，此函数提供了两个常量值： *pi* 和 *e*。

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

调用函数别名的结果如下所示。 

```dbgcmd
0:000> !constants
@$constants()                 : [object Object]
    math_constants   : [object Object]
    description      : Archimedes' pi and Euler's number e
```

将自动生成指向复杂对象的 DML 链接。 单击上面显示的 math_constants 将生成以下输出。 

```dbgcmd
0:000> dx -r1 @$constants().math_constants
@$constants().math_constants                 : [object Object]
    pi               : 3.141593
    e                : 2.718282
```


如果函数具有参数，则可以在函数别名命令本身之后提供。 请注意，函数别名命令后的一切都被视为表达式，并按这样的方式进行计算。 文本字符串不会直接传递到函数。 对于单个自变量表达式，它可以出现在函数别名命令本身之后。 对于多个自变量，应将其作为函数调用，如下面的示例中所示。


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

可以按如下所示调用这两个函数。

```dbgcmd
0:000> !neg 42
@$neg(42)        : -42

0:000> !add (5, 7)
@$add(5, 7)      : 0xc
```


## <a name="function-alias-use-with-the-dx-expression-evaluator"></a>用于 dx 表达式计算器的函数别名

除了调试扩展外 **！** 用于调用别名函数的 "感叹号" 命令语法，在按如下所示为前缀的情况下，与函数别名关联的所有名称将直接在 dx 表达式计算器中可用 *@$* 。  

```dbgcmd
0:000> dx @$neg(42)
@$neg(42)        : -42

0:000> dx @$add(99, 77)
@$add(99, 77)    : 0xb0
```


## <a name="function-alias-design-considerations"></a>函数别名设计注意事项

函数别名绝不应是公开绝大部分数据模型扩展中的功能的唯一方法。 数据模型扩展 (在 c + + 或 JavaScript) ，几乎总是应始终包含与类型或其他调试器概念关联的数据。 与进程关联的任务应该位于该对象的 "调试程序" 或子命名空间下。 函数别名可以方便地 (或转换可能需要更长时间查询的) 数据。 

作为内核模式示例，以下查询采用 PnP 设备树，并将其平展到简单的简单设备列表中： 

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

此 JavaScript 代码显示了如何以函数别名的形式实现此功能。 

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

然后，可以将函数别名称为调试扩展命令。 

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

使用函数别名的优点之一是可以使用 dx 语法进一步改进。 在此示例中，添加了一个 where 子句来查找包含 "硬盘" 的设备节点。

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


LINQ 命令（如下所示）可用于功能别名。All、。Any、。计数、。首先，。平展，。GroupBy，。Last。OrderBy，。OrderByDescending、。选择 "与"。其中. 这些方法) c # LINQ 方法形式 (尽可能严格地遵循这些方法。 有关详细信息，请参阅 [将 LINQ 与调试器对象配合使用](./using-linq-with-the-debugger-objects.md)。



**网格显示**

与其他 dx 命令一样，你可以在命令执行之后右键单击该命令，然后单击 "显示为网格" 或将 "-g" 添加到命令以获取结果的网格视图。 然后，可以单击任何要排序的列，例如在 InstancePath 上。

```dbgcmd
0: kd> dx -g @$devices().OrderBy(obj => obj.@"InstancePath")
```

![调试器对象函数显示已排序行的别名网格输出](images/debugger-objects-function-alias.png) 



## <a name="process-threads-example"></a>进程线程示例

调试器对象投影到以 "调试器" 为根的命名空间中。 进程、模块、线程、堆栈、堆栈帧和局部变量均可在 LINQ 查询中使用。

此示例 JavaScript 演示如何显示当前会话进程的线程计数：

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
这会显示带有！处理函数别名。


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
在此示例中，显示最大线程数最多的前5个进程。

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



## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[dx（显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[将 LINQ 与调试器对象配合使用](using-linq-with-the-debugger-objects.md)

[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md) 

---