---
title: JavaScript 扩展中的本机调试器对象
description: 本机调试器对象表示调试器环境的各种构造和行为。 对象可以传递到 (中，也可以在) JavaScript 扩展中获取。
ms.date: 09/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: f12f819968c3bdf85d48d75337dbef4b63c0bf5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792403"
---
# <a name="native-debugger-objects-in-javascript-extensions"></a>JavaScript 扩展中的本机调试器对象


本机调试器对象表示调试器环境的各种构造和行为。 对象可以传递到 (中，也可以在) JavaScript 扩展中获取，以操作调试器的状态。

示例调试器对象包括以下各项。

-   会话
-   线程/线程
-   进程/进程
-   堆栈帧/堆栈帧
-   局部变量
-   模块/模块
-   实用工具
-   状态
-   设置

例如，host.namespace.Debugger.Utility.Control.ExecuteCommand 对象可用于将 u 命令发送到带有以下两行 JavaScript 代码的调试器。

```dbgcmd
var ctl = host.namespace.Debugger.Utility.Control;   
var outputLines = ctl.ExecuteCommand("u");
```

本主题介绍如何使用常见对象并提供有关其属性和行为的参考信息。

有关使用 JavaScript 的常规信息，请参阅 [Javascript 调试器脚本](javascript-debugger-scripting.md)。 有关使用调试器对象的 JavaScript 示例，请参阅 [Javascript 调试器示例脚本](javascript-debugger-example-scripts.md)。 有关使用设置对象的信息，请参阅 [**。 "设置" (设置 "调试设置")**](-settings--set-debug-settings-.md)。

若要浏览调试器会话中可用的对象，请使用 [**dx (显示 NatVis Expression)**](dx--display-visualizer-variables-.md) 命令。 例如，可以通过此 dx 命令显示顶级调试器对象的某些对象。

```dbgcmd
0: kd> dx -r2 Debugger
Debugger                
    Sessions         : [object Object]
        [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{NET:Port=50000,Key=1.2.3.4,Target}
    Settings        
        Debug           
        Display         
        EngineInitialization
        Extensions      
        Input           
        Sources         
        Symbols         
        AutoSaveSettings : false
    State           
        DebuggerVariables
        PseudoRegisters 
        Scripts         
        UserVariables   
    Utility         
        Collections     
        Control         
        Objects   
```

上面列出的所有项都是可单击的 DML，可以进一步 recursed 以查看调试器对象结构。

## <a name="span-idextendingspanspan-idextendingspanspan-idextendingspanextending-the-debugger-via-the-data-model"></a><span id="Extending"></span><span id="extending"></span><span id="EXTENDING"></span>通过数据模型扩展调试器


调试器数据模型允许创建一个接口，以获取有关 Windows 中具有以下属性的应用程序和驱动程序的信息。

-   可发现和组织-可以使用 dx 命令查询逻辑结构化命名空间。
-   可以使用 LINQ 查询-这允许使用标准查询语言对数据进行提取和排序。
-   可以使用本主题中所述的技术以逻辑方式一致地扩展扩展，并使用调试器脚本提供程序（例如 Natvis 和 JavaScript）。

## <a name="span-idextending-debugger-objectspanspan-idextending-debugger-objectspanspan-idextending-debugger-objectspanextending-a-debugger-object-in-javascript"></a><span id="Extending-Debugger-Object"></span><span id="extending-debugger-object"></span><span id="EXTENDING-DEBUGGER-OBJECT"></span>在 JavaScript 中扩展调试器对象

除了能够在 JavaScript 中创建可视化工具外，脚本扩展还可以修改调试器的核心概念：会话、进程、线程、堆栈、堆栈帧、局部变量，甚至将自身发布为其他扩展可以使用的扩展点。

本部分介绍如何在调试器中扩展核心概念。 为共享而构建的扩展应符合 [JavaScript 扩展中的本机调试器对象中提供的指导原则-设计和测试注意事项](native-objects-in-javascript-extensions-design-considerations.md)。

**注册扩展**

脚本可以通过 initializeScript 方法中返回的数组中的条目注册提供扩展的事实。

```dbgcmd
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process")];
}
```

在返回的数组中存在 namedModelParent 对象向调试器指出给定的原型对象或 ES6 类 (comProcessExtension，在这种情况下) 会成为在名称调试器中注册的模型的父数据模型。

**调试器对象扩展点**

以下调试器扩展点是调试器所必不可少的，可供脚本提供程序（如 JavaScript）使用。

"**调试程序"。会话**：会话的列表 (调试器附加到的目标) 

KD **：将调试器附加** 到 (实时用户模式、等的单个会话 (目标) ) 

**调试程序**：会话内的进程列表

**调试程序. 模型**：进程中的线程列表

"**调试器**"：进程中的单个线程 (无论用户模式还是内核模式) 

**调试程序. 模型**：线程的堆栈

**StackFrames**：组成堆栈的帧的集合

**堆栈帧**：堆栈内的单独堆栈帧

**LocalVariables**：堆栈帧中的局部变量

**调试程序. 参数**：堆栈帧中的调用参数

**调试程序. 模块**：进程的地址空间中的单个模块


 

**附加数据模型对象**

此外，还提供了一些由核心数据模型定义的其他数据模型对象。

**DataModel**：内部数值 (序数、浮点数等 .。。) 

**DataModel**：字符串

**DataModel**：本机数组

**DataModel**： guid

**DataModel**：错误对象

**DataModel 可迭代**：应用于每个可迭代的对象

**DataModel**：应用于具有显示字符串转换的每个对象


 

**示例 COM 调试器对象扩展概述**

我们分析一个示例。 假设要创建一个调试器扩展来显示特定于 COM 的信息，例如全局接口表 (GIT) 。

过去，可能有一个现有的调试器扩展，其中包含许多命令，这些命令提供了一种方法来访问 COM。 一个命令可能会 () 实例的全局接口表中显示以进程为中心的信息。 另一个命令可以提供以线程为中心的信息，例如在中执行的单元代码。 你可能需要了解并加载另一个调试器扩展，以探索 COM 的其他方面。

JavaScript 扩展可以修改进程和线程的概念，而不是使用一组难于发现的命令，而是以一种自然、可探索对象且可组合的方式将此信息添加到其他调试器扩展。

**用户或内核模式调试器对象扩展**

调试器和调试器对象在用户模式和内核模式下具有不同的行为。 创建调试器模型对象时，需要确定将使用的环境。 由于我们将在用户模式下使用 COM，因此，我们将在用户模式下创建和测试此 com 扩展。 在其他情况下，可以创建可在用户和内核模式调试中使用的调试器 JavaScript。

**创建子命名空间**

回到我们的示例，我们可以定义一个 prototype 或 ES6 类， *comProcessExtension* ，其中包含我们要添加到 process 对象的一组对象。

**重要提示**   使用子命名空间的目的是创建逻辑结构化的自然可探索对象范例。 例如，避免将无关项转储到相同的子命名空间中。 在创建子命名空间之前，请仔细查看 [JavaScript 扩展中的本机调试器对象中讨论的信息-设计和测试注意事项](native-objects-in-javascript-extensions-design-considerations.md) 。

在此代码片段中，我们将在现有的进程调试器对象上创建名为 "COM" 的子命名空间。

```javascript
var comProcessExtension =
{
    //
    // Add a sub-namespace called 'COM' on process.
    //
    get COM()
    {
        //
        // What is 'this' below...?  It's the debugger's process object.  Yes -- this means that there is a cross-language
        // object hierarchy here.  A C++ object implemented in the debugger has a parent model (prototype) which is
        // implemented in JavaScript.
        //
        return new comNamespace(this);
    }
}
```

**命名空间实现**

接下来，在进程上创建实现子命名空间 COM 的对象。

**重要说明**  
无论附加到用户模式还是 KD) ，都可以有多个进程 (。 此扩展无法假定调试器的当前状态为用户预期的状态。 有人可以 &lt; &gt; 在变量中捕获 someProcess 并对其进行修改，这可能会导致显示错误的进程上下文中的信息。 解决方法是在扩展中添加代码，以便每个实例化将跟踪它附加到的进程。 对于此代码示例，通过属性的 "this" 指针传递此信息。

`this.__process = process;`

 

```javascript
class comNamespace
{
    constructor(process)
    {
        //
        // This is an entirely JavaScript object.  Each instantiation of a comNamespace will keep track
        // of what process it is attached to (passed via the ''this'' pointer of the property getter
        // we authored above.
        //
        this.__process = process;
    }
    
    get GlobalObjects()
    {
        return new globalObjects(this.__process);
    }
}
```

**COM 全局接口表的实现逻辑**

为了更清晰地分离出 COM 全局接口表的实现逻辑，我们将定义一个 ES6 类， *gipTable* ，它将抽象掉 com GIP 表和另一个 *globalObjects*，后者将从上面所示的命名空间实现代码段中定义的 globalObjects ( # A1 getter 返回。 所有这些详细信息都可以隐藏在 initializeScript 的闭包中，以避免将其中的任何内部详细信息发布到调试器命名空间中。

```javascript
// gipTable:
//
// Internal class which abstracts away the GIP Table.  It iterates objects of the form
// {entry : GIPEntry, cookie : GIT cookie}
//
class gipTable
{
    constructor(gipProcess)
    {
        //
        // Windows 8 through certain builds of Windows 10, it's in CGIPTable::_palloc.  In certain builds
        // of Windows 10 and later, this has been moved to GIPEntry::_palloc.  We need to check which.
        //
        var gipAllocator = undefined;
        try
        {
            gipAllocator = host.getModuleSymbol("combase.dll", "CGIPTable::_palloc", "CPageAllocator", gipProcess)._pgalloc;
        }
        catch(err)
        {
        }

        if (gipAllocator == undefined)
        {
            gipAllocator = host.getModuleSymbol("combase.dll", "GIPEntry::_palloc", "CPageAllocator", gipProcess)._pgalloc;
        }

        this.__data = {
            process : gipProcess,
            allocator : gipAllocator,
            pageList : gipAllocator._pPageListStart,
            pageCount : gipAllocator._cPages,
            entriesPerPage : gipAllocator._cEntriesPerPage,
            bytesPerEntry : gipAllocator._cbPerEntry,
            PAGESHIFT : 16,
            PAGEMASK : 0x0000FFFF,
            SEQNOMASK : 0xFF00
        };
    }

    *[Symbol.iterator]()
    {
        for (var pageNum = 0; pageNum < this.__data.pageCount; ++pageNum)
        {
            var page = this.__data.pageList[pageNum];
            for (var entryNum = 0; entryNum < this.__data.entriesPerPage; ++entryNum)
            {
                var entryAddress = page.address.add(this.__data.bytesPerEntry * entryNum);
                var gipEntry = host.createPointerObject(entryAddress, "combase.dll", "GIPEntry *", this.__data.process);
                if (gipEntry.cUsage != -1 && gipEntry.dwType != 0)
                {
                    yield {entry : gipEntry, cookie : (gipEntry.dwSeqNo | (pageNum << this.__data.PAGESHIFT) | entryNum)};
                }
            }
        }
    }

    entryFromCookie(cookie)
    {
        var sequenceNo = (cookie & this.__data.SEQNOMASK);
        cookie = cookie & ~sequenceNo;
        var pageNum = (cookie >> this.__data.PAGESHIFT);
        if (pageNum < this.__data.pageCount)
        {
            var page = this.__data.pageList[pageNum];
            var entryNum = (cookie & this.__data.PAGEMASK);
            if (entryNum < this.__data.entriesPerPage)
            {
                var entryAddress = page.address.add(this.__data.bytesPerEntry * entryNum);
                var gipEntry = host.createPointerObject(entryAddress, "combase.dll", "GIPEntry *", this.__data.process);
                if (gipEntry.cUsage != -1 && gipEntry.dwType != 0 && gipEntry.dwSeqNo == sequenceNo)
                {
                    return {entry : gipEntry, cookie : (gipEntry.dwSeqNo | (pageNum << this.__data.PAGESHIFT) | entryNum)};
                }
            }
        }

        //
        // If this exception flows back to C/C++, it will be a failed HRESULT (according to the type of error -- here E_BOUNDS)
        // with the message being encapsulated by an error object.
        //
        throw new RangeError("Unable to find specified value");
    }
}





// globalObjects:
//
// The class which presents how we want the GIP table to look to the data model.  It iterates the actual objects
// in the GIP table indexed by their cookie.
//
class globalObjects
{
    constructor(process)
    {
        this.__gipTable = new gipTable(process);
    }

    *[Symbol.iterator]()
    {
        for (var gipCombo of this.__gipTable)
        {
            yield new host.indexedValue(gipCombo.entry.pUnk, [gipCombo.cookie]);
        }
    }

    getDimensionality()
    {
        return 1;
    }

    getValueAt(cookie)
    {
        return this.__gipTable.entryFromCookie(cookie).entry.pUnk;
    }
}
```

最后，使用 namedModelRegistration 注册新的 COM 功能。

```javascript
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process"),
            new host.namedModelRegistration(comNamespace, "Debugger.Models.ComProcess")];
}
```

将代码保存到使用记事本之类的应用程序 GipTableAbstractor.js。

下面是加载此扩展之前用户模式下可用的进程信息。

```dbgcmd
0:000:x86> dx @$curprocess
@$curprocess                 : DataBinding.exe
    Name             : DataBinding.exe
    Id               : 0x1b9c
    Threads         
    Modules  
```

加载 JavaScript 脚本提供程序和扩展。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\GipTableAbstractor.js
JavaScript script successfully loaded from 'C:\JSExtensions\GipTableAbstractor.js'
```

然后，使用 dx 命令显示有关使用预定义的 @ $curprocess 的进程的信息。

```dbgcmd
0:000:x86> dx @$curprocess
@$curprocess                 : DataBinding.exe
    Name             : DataBinding.exe
    Id               : 0x1b9c
    Threads         
    Modules         
    COM              : [object Object]
```

```dbgcmd
0:000:x86> dx @$curprocess.COM
@$curprocess.COM                 : [object Object]
    GlobalObjects    : [object Object]
0:000:x86> dx @$curprocess.COM.GlobalObjects
@$curprocess.COM.GlobalObjects                 : [object Object]
    [0x100]          : 0x12f4fb0 [Type: IUnknown *]
    [0x201]          : 0x37cfc50 [Type: IUnknown *]
    [0x302]          : 0x37ea910 [Type: IUnknown *]
    [0x403]          : 0x37fcfe0 [Type: IUnknown *]
    [0x504]          : 0x12fe1d0 [Type: IUnknown *]
    [0x605]          : 0x59f04e8 [Type: IUnknown *]
    [0x706]          : 0x59f0eb8 [Type: IUnknown *]
    [0x807]          : 0x59f5550 [Type: IUnknown *]
    [0x908]          : 0x12fe340 [Type: IUnknown *]
    [0xa09]          : 0x5afcb58 [Type: IUnknown *]
```

此表还可以通过 GIT cookie 以编程方式访问。

```dbgcmd
0:000:x86> dx @$curprocess.COM.GlobalObjects[0xa09]
@$curprocess.COM.GlobalObjects[0xa09]                 : 0x5afcb58 [Type: IUnknown *]
    [+0x00c] __abi_reference_count [Type: __abi_FTMWeakRefData]
    [+0x014] __capture        [Type: Platform::Details::__abi_CapturePtr]
```

**用 LINQ 扩展调试器对象概念**

除了能够扩展进程和线程之类的对象之外，JavaScript 还可以扩展与数据模型关联的概念。 例如，可以将新的 LINQ 方法添加到每个可迭代。 请考虑一个示例扩展，即 "DuplicateDataModel"，它会在可迭代 N 次中复制每个条目。 下面的代码演示如何实现此操作。

```javascript
function initializeScript()
{
    var newLinqMethod =
    {
        Duplicate : function *(n)
        {
            for (var val of this)
            {
                for (var i = 0; i < n; ++i)
                {
                    yield val;
                }
            };
        }
    };

    return [new host.namedModelParent(newLinqMethod, "DataModel.Models.Concepts.Iterable")];
}
```

将代码保存到使用记事本之类的应用程序 DuplicateDataModel.js。

如有必要，加载 JavaScript 脚本提供程序，然后加载 DuplicateDataModel.js 扩展。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\DuplicateDataModel.js
JavaScript script successfully loaded from 'C:\JSExtensions\DuplicateDataModel.js'
```

使用 dx 命令测试新的复制函数。

```dbgcmd
0: kd> dx -r1 Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d
Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d                 : [object Generator]
    [0]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [1]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [2]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
    [3]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
…
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[JavaScript 扩展中的本机调试器对象 - 调试器对象详细信息](native-objects-in-javascript-extensions-debugger-objects.md)

[JavaScript 扩展中的本机调试器对象-设计和测试注意事项](native-objects-in-javascript-extensions-design-considerations.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)
