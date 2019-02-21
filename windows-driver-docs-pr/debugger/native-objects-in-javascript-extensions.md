---
title: 中 JavaScript 扩展本机调试器对象
description: 本机调试器对象表示各种构造和调试器环境的行为。 对象可以是传递到 （或中获取） JavaScript 扩展。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEE8
ms.date: 12/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: d88712e1cf2fbe462320547b7d1af11cd06352f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520069"
---
# <a name="native-debugger-objects-in-javascript-extensions"></a>中 JavaScript 扩展本机调试器对象


本机调试器对象表示各种构造和调试器环境的行为。 对象可以是传递到 （或中获取） JavaScript 扩展操作调试器的状态。

如调试器对象包括以下内容。

-   会议
-   线程 / 线程
-   进程数 / 处理
-   堆栈帧 / 堆栈帧
-   本地变量
-   模块 / 模块
-   实用程序
-   状态
-   “设置”

例如 host.namespace.Debugger.Utility.Control.ExecuteCommand 对象可用于 u 命令发送到以下两行 JavaScript 代码的调试器。

```dbgcmd
var ctl = host.namespace.Debugger.Utility.Control;   
var outputLines = ctl.ExecuteCommand("u");
```

本主题介绍如何使用常用的对象，并提供有关其属性和行为参考信息。

[扩展数据模型通过调试器](#extending)

[扩展 JavaScript 中的调试器对象](#extending-debugger-object)

[JavaScript 扩展中的调试器对象](#debugger-objects)

[JavaScript 扩展的主机 Api](#host-apis)

[在 JavaScript 中的数据模型概念](#data-model)

[调试器数据模型设计注意事项](#design-considerations)

有关使用 JavaScript 的常规信息，请参阅[JavaScript 调试器脚本](javascript-debugger-scripting.md)。 有关使用调试程序对象的 JavaScript 示例，请参阅[JavaScript 调试器的示例脚本](javascript-debugger-example-scripts.md)。 有关使用设置对象的信息，请参阅[ **.settings （设置调试设置）**](-settings--set-debug-settings-.md)。

若要浏览在调试器会话中可用的对象，使用[ **dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md)命令。 例如，您可以显示一些与此 dx 命令的顶级级别调试器对象。

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

所有上面列出的项都是可单击 DML，可以将进行递归搜索进一步向调试器对象结构视图。

## <a name="span-idextendingspanspan-idextendingspanspan-idextendingspanextending-the-debugger-via-the-data-model"></a><span id="Extending"></span><span id="extending"></span><span id="EXTENDING"></span>扩展数据模型通过调试器


调试器数据模型可以创建的应用程序和具有以下属性的 Windows 中的驱动程序有关的信息的接口。

-   可发现并组织-可以使用 dx 命令查询逻辑结构的命名空间。
-   可以查询使用 LINQ-这样，用于提取和使用标准查询语言的数据排序。
-   可以是逻辑上一致地扩展-可扩展使用脚本编写提供程序，如 Natvis 和 JavaScript 的调试器与本主题中所述的技术。

## <a name="span-idextending-debugger-objectspanspan-idextending-debugger-objectspanspan-idextending-debugger-objectspanextending-a-debugger-object-in-javascript"></a><span id="Extending-Debugger-Object"></span><span id="extending-debugger-object"></span><span id="EXTENDING-DEBUGGER-OBJECT"></span>扩展 JavaScript 中的调试器对象


除了能够在 JavaScript 中创建可视化工具，脚本扩展还可以修改核心概念的调试器-会话、 进程、 线程、 堆栈、 堆栈帧，本地变量-和甚至发布本身，因为扩展点，其他可以使用扩展。

本部分介绍如何扩展该调试器内的核心概念。 生成共享的扩展应遵守中提供的指导[调试器的数据模型设计注意事项](#design-considerations)。

**注册扩展**

脚本可以注册这一事实，它提供了通过从 initializeScript 方法返回的数组中的条目的扩展。

```dbgcmd
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process")];
}
```

向调试器指示返回的数组中的 host.namedModelParent 对象存在给定的原型对象或 ES6 类 (在此情况下 comProcessExtension) 将父数据模型的模型的名称注册到Debugger.Models.Process。

**调试器对象扩展点**

下面的调试器扩展点是调试器的必要组成部分，并可用于通过 JavaScript 等脚本提供程序使用。

|                                |                                                                                              |
|--------------------------------|----------------------------------------------------------------------------------------------|
| Debugger.Models.Sessions       | 将调试器附加到的会话 （目标） 的列表                              |
| Debugger.Models.Session        | 将调试器附加到的单个会话 （目标） (实时用户模式下，KD，等等。...) |
| Debugger.Models.Processes      | 某个会话中的进程的列表                                                       |
| Debugger.Models.Threads        | 在进程中线程的列表                                                         |
| Debugger.Models.Thread         | 进程内的单个线程 (无论用户或内核模式)            |
| Debugger.Models.Stack          | 线程的堆栈                                                                        |
| Debugger.Models.StackFrames    | 构成一个堆栈帧的集合                                               |
| Debugger.Models.StackFrame     | 在堆栈中各个堆栈帧                                                     |
| Debugger.Models.LocalVariables | 堆栈帧中的本地变量                                                     |
| Debugger.Models.Parameters     | 调用堆栈帧中的参数                                               |
| Debugger.Models.Module         | 进程的地址空间中的单个模块                                   |

 

**其他数据模型对象**

此外，还有一些其他数据模型对象定义的核心数据模型。

|                                             |                                                               |
|---------------------------------------------|---------------------------------------------------------------|
| DataModel.Models.Intrinsic                  | 一个内部值 (序号、 浮点数，等等。...)                 |
| DataModel.Models.String                     | 一个字符串，                                                      |
| DataModel.Models.Array                      | 本机数组                                                |
| DataModel.Models.Guid                       | 一个 GUID                                                        |
| DataModel.Models.Error                      | 错误对象                                               |
| DataModel.Models.Concepts.Iterable          | 应用于它是可迭代每个对象                     |
| DataModel.Models.Concepts.StringDisplayable | 应用于每个对象具有显示字符串转换 |

 

**示例 COM 调试器对象扩展概述**

举个例子。 假设你想要创建要向 COM，显示特定的信息，如全局接口表 (GIT) 的调试器扩展。

在过去，可能存在许多命令提供一种方法访问 com。 关于内容的现有调试器扩展 一个命令可能会显示进程中心的信息 （全局接口表实例）。 另一个命令中可能提供如单元的代码执行中的线程为中心信息。 可能需要了解的有关并加载要浏览的 com。 其他方面的第二个调试器扩展

而不是让一系列难以发现命令，JavaScript 扩展可以修改的内容的进程和线程，是自然、 可探索对象，并与其他调试程序扩展可组合的方式添加此信息的调试程序的概念。

**用户或内核模式调试程序对象扩展**

调试器和调试器对象具有不同的行为在用户和内核模式下。 创建您的调试器模型对象时，您需要决定要使用中的环境。 因为我们将使用 COM 在用户模式下，我们将创建并在用户模式下测试此 com 扩展。 在其他情况下，您可能能够创建以用户模式和内核模式调试的调试程序将处理的 JavaScript。

**创建子 Namespace**

回到我们的示例中，我们可以定义原型或 ES6 类*comProcessExtension*其中包含的功能，我们想要添加到将进程对象。

**重要**  与子命名空间的目的是创建一种逻辑结构和自然可探索对象的模式。 例如，避免转储到同一个子命名空间不相关的项。 请仔细查看的信息中所述[调试器的数据模型设计注意事项](#design-considerations)之前创建一个子命名空间。

 

在此代码片段中，我们将创建添加到现有进程调试器对象称为 COM 的子命名空间。

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

**Namespace 实现**

接下来，创建进程实现子命名空间 COM 的对象。

**重要**  可以有多个进程 （无论是附加到此类在用户模式下或在 KD）。 此扩展不能假定调试器的当前状态是什么适用的用户。 有人可以捕获&lt;someProcess&gt;.COM 的变量中并对其进行修改，这可能会导致错误的进程上下文中呈现信息。 解决方案是将代码添加的扩展中，以便每个实例化跟踪的附加到的进程。 有关此代码示例中，将通过该属性的 this 指针传递此信息。

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

若要将此 COM 全局接口表的实现逻辑更清楚地，我们将定义一个 ES6 类*gipTable*其抽象化 COM GIP 表，另一个， *globalObjects*，从上面所示 Namespace 实现代码段中定义的 GlobalObjects() getter 将返回内容。 所有这些详细信息可以隐藏在 initializeScript 以避免任何出这些内部详细信息发布到调试程序命名空间的闭包。

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

最后，使用 host.namedModelRegistration 注册新的 COM 功能。

```javascript
function initializeScript()
{
    return [new host.namedModelParent(comProcessExtension, "Debugger.Models.Process"),
            new host.namedModelRegistration(comNamespace, "Debugger.Models.ComProcess")];
}
```

将代码保存到 GipTableAbstractor.js 使用记事本之类的应用程序。

下面是进程信息在用户模式下可用之前加载此扩展。

```dbgcmd
0:000:x86> dx @$curprocess
@$curprocess                 : DataBinding.exe
    Name             : DataBinding.exe
    Id               : 0x1b9c
    Threads         
    Modules  
```

加载脚本编写提供程序和扩展的 JavaScript。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\GipTableAbstractor.js
JavaScript script successfully loaded from 'C:\JSExtensions\GipTableAbstractor.js'
```

然后使用 dx 命令显示有关使用预定义的 @$ curprocess 过程的信息。

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

此表而言也是以编程方式访问通过 GIT cookie。

```dbgcmd
0:000:x86> dx @$curprocess.COM.GlobalObjects[0xa09]
@$curprocess.COM.GlobalObjects[0xa09]                 : 0x5afcb58 [Type: IUnknown *]
    [+0x00c] __abi_reference_count [Type: __abi_FTMWeakRefData]
    [+0x014] __capture        [Type: Platform::Details::__abi_CapturePtr]
```

**使用 LINQ 的扩展调试器对象概念**

除了能够扩展对象，如进程和线程，JavaScript 可以扩展与数据模型以及相关联的概念。 例如，就可以将新的 LINQ 方法添加到每个迭代。 每个条目中可迭代的 N 次的重复项，请考虑示例扩展，"DuplicateDataModel"。 下面的代码演示如何实现此操作。

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

将代码保存到 DuplicateDataModel.js 使用记事本之类的应用程序。

加载 JavaScript 提供脚本程序如有必要，然后加载 DuplicateDataModel.js 扩展。

```dbgcmd
0:000:x86> !load jsprovider.dll
0:000:x86> .scriptload C:\JSExtensions\DuplicateDataModel.js
JavaScript script successfully loaded from 'C:\JSExtensions\DuplicateDataModel.js'
```

使用 dx 命令来测试新的重复函数。

```dbgcmd
0: kd> dx -r1 Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d
Debugger.Sessions.First().Processes.First().Threads.Duplicate(2),d                 : [object Generator]
    [0]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [1]              : nt!DbgBreakPointWithStatus (fffff800`9696ca60) 
    [2]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
    [3]              : intelppm!MWaitIdle+0x18 (fffff805`0e351348) 
…
```

## <a name="span-iddebugger-objectsspanspan-iddebugger-objectsspanspan-iddebugger-objectsspandebugger-objects-in-javascript-extensions"></a><span id="Debugger-Objects"></span><span id="debugger-objects"></span><span id="DEBUGGER-OBJECTS"></span>JavaScript 扩展中的调试器对象


**传递本机对象**

可以传递到或 JavaScript 扩展中通过多种方式获取调试器对象。

-   它们可以传递给 JavaScript 函数或方法
-   它们可以是 JavaScript 原型的实例对象 (作为可视化工具，例如)
-   它们可以从主机方法用于创建本机调试器对象返回
-   它们可以返回从主机方法用于创建本机对象的调试器

传递给 JavaScript 扩展的调试器对象具有一组的此部分中描述的功能。

-   属性访问
-   投影的名称
-   与本机调试器对象相关的特殊类型
-   其他属性

**属性访问**

尽管由 JavaScript 提供程序本身放置的对象上有一些属性，输入 JavaScript 本机对象上的属性大部分由数据模型提供。 这意味着，对于属性访问---object.propertyName 或对象\[propertyName\]，会出现以下情况。

-   如果*propertyName*的属性名称投影到对象上由 JavaScript 提供程序本身，它将解析为这第一次; 否则为
-   如果*propertyName*密钥的名称投影到对象上由数据模型 （另一个可视化工具），它能解析此名称到第二个; 否则为
-   如果*propertyName*是名称的本机对象的字段，它能解析此名称到第三个; 否则为
-   如果对象是一个指针，将取消引用指针，并且上述周期将继续 （取消引用对象后跟跟本机字段的键的投影的属性）

在 JavaScript 中-object.propertyName 和对象的属性访问的正常方式\[propertyName\] -将访问的对象的基础本机字段一样使用 dx 命令将该调试器内。

**投影的名称**

以下属性 （和方法） 将投影到其输入 JavaScript 本机对象。

| 方法             | 签名                  | 描述                                                                                                                                |
|--------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| hostContext        | 属性                   | 返回一个对象，它表示对象中的上下文 (地址空间、 调试目标，等等。...)                              |
| targetLocation     | 属性                   | 返回一个对象是一个抽象概念的其中对象是在地址空间内 (虚拟地址、 注册、 子寄存器，等等。...) |
| targetSize         | 属性                   | 返回对象的大小 (有效地： sizeof (&lt;类型的对象&gt;)                                                                |
| addParentModel     | .addParentModel(object)    | 向对象添加新的父模型 （类似于 JavaScript 原型，但数据 mdoel 端）                                          |
| removeParentModel  | .removeParentModel(object) | 从对象中移除给定的父模型                                                                                               |
| runtimeTypedObject | 属性                   | 在对象上执行分析，并尝试将其转换为 （派生程度最高） 的运行时类型                                                 |

 

如果对象是一个指针，以下属性 （和方法） 被投影到输入 JavaScript 的指针：

| 属性名称 | 签名      | 描述                                                                    |
|---------------|----------------|--------------------------------------------------------------------------------|
| 添加           | .add(value)    | 执行指针的指针和指定的值之间的数学加法运算     |
| 地址       | 属性       | 返回指针的地址作为 64 位序号对象 （库类型） |
| 取消引用   | .dereference() | 取消引用指针，并返回基础对象                     |
| isNull        | 属性       | 返回的指针值是 nullptr (0)                        |

 

**与本机调试器对象相关的特殊类型**

**位置对象**

从本机对象的 targetLocation 属性返回的位置对象包含以下属性 （和方法）。

| 属性名称 | 签名        | 描述                                          |
|---------------|------------------|------------------------------------------------------|
| 添加           | .add(value)      | 将绝对的字节偏移量添加到的位置。        |
| 相减      | .subtract(value) | 减去一个绝对的字节偏移量位置。 |

 

**其他属性**

**Iterability**

为可迭代的数据模型理解的任何对象 (它是本机数组或具有可视化工具 (NatVis 或其他) 从而可迭代) 会置于其上一个迭代器函数 （通过 ES6 标准 Symbol.iterator 编制索引）。 这意味着您可以按如下所示循环访问在 JavaScript 中的本机对象。

```javascript
function iterateNative(nativeObject)
{
    for (var val of nativeObject)
    {
        // 
        // val will contain each element iterated from the native object.  This would be each element of an array,
        // each element of an STL structure which is made iterable through NatVis, each element of a data structure
        // which has a JavaScript iterator accessible via [Symbol.iterator], or each element of something
        // which is made iterable via support of IIterableConcept in C/C++.
        //
    }
}
```

**可索引性**

被理解为可索引序号通过一个维度中的对象 (例如： 本机数组) 将会在 JavaScript 中通过标准属性访问运算符可编制索引-对象\[索引\]。 如果可编制索引的名称或多个维度中可编制索引的对象，getValueAt 和 setValueAt 方法将投影到对象上，以便 JavaScript 代码可以利用索引器。

```javascript
function indexNative(nativeArray)
{
    var first = nativeArray[0];
}
```

**字符串转换**

它具有显示的字符串转换通过支持 IStringDisplayableConcept 或 NatVis DisplayString 元素的任何本机对象将具有可通过标准的 JavaScript toString 方法访问该字符串转换。

```javascript
function stringifyNative(nativeObject)
{
    var myString = nativeObject.toString();
}
```

## <a name="span-idcreatingnativedebuggerobjectsspanspan-idcreatingnativedebuggerobjectsspanspan-idcreatingnativedebuggerobjectsspancreating-native-debugger-objects"></a><span id="Creating_Native_Debugger_Objects"></span><span id="creating_native_debugger_objects"></span><span id="CREATING_NATIVE_DEBUGGER_OBJECTS"></span>创建本机调试器对象


如前文所述，JavaScript 脚本可以通过将传递到几种方式之一中的 JavaScript 获取对本机对象的访问权限或它可以通过调用程序主机库创建它们。 使用以下函数创建本机调试器对象。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">方法</th>
<th align="left">签名</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>host.getModuleSymbol</p></td>
<td align="left"><p>getModuleSymbol(moduleName, symbolName, [contextInheritor])</p>
<p>getModuleSymbol(moduleName, symbolName, [typeName], [contextInheritor])</p></td>
<td align="left"><p>返回一个对象，用于为特定模块内的全局符号。 模块名称和符号名称的字符串。</p>
<p>如果可选<em>contextInheritor</em>提供自变量、 模块和符号将查找中传递的对象在同一上下文 （调试目标中的地址空间）。 如果未提供参数，模块和符号将查找在调试器中&#39;s 当前上下文。 这不是一次性的测试脚本的 JavaScript 扩展应始终提供显式的上下文。</p>
<p>如果可选<em>typeName</em>提供参数，该符号将假定为传递的类型的将忽略了符号中指示的类型。 注意： 任何调用方需要对公共符号的模块进行操作，应始终提供显式类型名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>host.createPointerObject</p></td>
<td align="left"><p>createPointerObject(address, moduleName, typeName, [contextInheritor])</p></td>
<td align="left"><p>创建在指定的地址或位置的指针对象。 模块名称和类型名称是字符串。</p>
<p>如果可选<em>contextInheritor</em>提供自变量、 模块和符号将查找中传递的对象在同一上下文 （调试目标中的地址空间）。 如果未提供参数，模块和符号将查找在调试器中&#39;s 当前上下文。 这不是一次性的测试脚本的 JavaScript 扩展应始终提供显式的上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>host.createTypedObject</p></td>
<td align="left"><p>createTypedObject(location, moduleName, typeName, [contextInheritor])</p></td>
<td align="left"><p>创建一个对象表示的调试目标中的指定位置的地址空间中的本机类型化的对象。 模块名称和类型名称是字符串。</p>
<p>如果可选<em>contextInheritor</em>提供自变量、 模块和符号将查找中传递的对象在同一上下文 （调试目标中的地址空间）。 如果未提供参数，模块和符号将查找在调试器中&#39;s 当前上下文。 这不是一次性的测试脚本的 JavaScript 扩展应始终提供显式的上下文。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idhost-apisspanspan-idhost-apisspanspan-idhost-apisspanhost-apis-for-javascript-extensions"></a><span id="Host-APIs"></span><span id="host-apis"></span><span id="HOST-APIS"></span>JavaScript 扩展的主机 Api


JavaScript 提供程序插入到此操作将它加载每个脚本的全局命名空间中被称为主机的对象。 此对象提供对脚本的关键功能的访问权限，以及到调试器的命名空间的访问。 它是在两个阶段中设置的。

-   **阶段 1**:执行任何脚本之前，该主机对象仅包含要初始化自身并注册其可扩展性点 （同时作为生成者和使用者） 的脚本所需功能的最小集。 根和初始化代码并非用于操作的调试目标状态或执行复杂的操作，并且，在这种情况下，主机未完全填充之前 initializeScript 方法返回之后。

-   **阶段 2**:InitializeScript 返回后，该主机对象被填充所需操作的调试目标状态的一切。

**主机对象级别**

几个关键功能是直接在该主机对象。 其余部分是子命名空间。 命名空间包括以下内容。

| 命名空间   | 描述                                                              |
|-------------|--------------------------------------------------------------------------|
| 诊断 | 若要帮助诊断和调试的脚本代码的功能    |
| memory      | 启用内存读取和写入调试目标内的功能 |

 

**根级别**

直接在该主机对象，以下属性、 方法和构造函数可以找到。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名称</th>
<th align="left">签名</th>
<th align="left">阶段存在</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">createPointerObject</td>
<td align="left"><p>createPointerObject(address, moduleName, typeName, [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">创建在指定的地址或位置的指针对象。 模块名称和类型名称是字符串。 可选<strong>contextInheritor</strong>参数的工作方式与 getModuleSymbol 一样。</td>
</tr>
<tr class="even">
<td align="left">createTypedObject</td>
<td align="left"><p>createTypedObject(location, moduleName, typeName, [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">创建一个对象表示的调试目标中的指定位置的地址空间中的本机类型化的对象。 模块名称和类型名称是字符串。 可选 contextInheritor 参数的工作方式与 getModuleSymbol 一样。</td>
</tr>
<tr class="odd">
<td align="left">currentProcess</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">返回表示调试器的当前进程的对象</td>
</tr>
<tr class="even">
<td align="left">currentSession</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">返回表示调试器的当前会话的对象的目标、 转储 (等...） 在调试</td>
</tr>
<tr class="odd">
<td align="left">currentThread</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">返回表示调试器的当前线程的对象</td>
</tr>
<tr class="even">
<td align="left">evaluateExpression</td>
<td align="left"><p>evaluateExpression(expression, [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">这会调用调试主机来计算表达式使用的语言来仅限调试目标。 如果可选<em>contextInheritor</em>提供参数，将在上下文中计算表达式 (例如： 地址空间和调试目标) 的参数; 否则，它将被计算在调试器的当前上下文中</td>
</tr>
<tr class="odd">
<td align="left">evaluateExpressionInContext</td>
<td align="left"><p>evaluateExpressionInContext(context, expression)</p></td>
<td align="left">2</td>
<td align="left">这会调用调试主机来计算表达式使用的语言来仅限调试目标。 上下文参数指示的隐式计算利用此指针。 将上下文中计算表达式 (例如： 地址空间和调试目标) 为由<em>上下文</em>参数。</td>
</tr>
<tr class="even">
<td align="left">getModuleSymbol</td>
<td align="left"><p>getModuleSymbol(moduleName, symbolName, [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">返回一个对象，用于为特定模块内的全局符号。 模块名称和符号名称的字符串。 如果可选<em>contextInheritor</em>提供自变量、 模块和符号将查找中传递的对象在同一上下文 （调试目标中的地址空间）。 如果未提供参数，模块和符号将查找在调试器中&#39;s 当前上下文。 这不是一次性脚本了 JavaScript 扩展应始终提供显式上下文</td>
</tr>
<tr class="odd">
<td align="left">getNamedModel</td>
<td align="left"><p>getNamedModel(modelName)</p></td>
<td align="left">2</td>
<td align="left">返回针对具有给定名称已注册的数据模型。 请注意，它是完全合法称之为针对尚未注册的名称。 执行此操作将创建该名称的存根和存根 （stub） 的操作不会对在注册时的实际对象</td>
</tr>
<tr class="even">
<td align="left">indexedValue</td>
<td align="left"><p>new indexedValue(value, indicies)</p></td>
<td align="left">2</td>
<td align="left">若要将一组默认的索引分配给迭代的值可以从 JavaScript 迭代器中返回的对象的构造函数。 索引集必须表示为 JavaScript 数组。</td>
</tr>
<tr class="odd">
<td align="left">Int64</td>
<td align="left"><p>新的 Int64 （value，[highValue]）</p></td>
<td align="left">1</td>
<td align="left">此代码构造的库 Int64 类型。 单参数版本将使用它可以打包到 int64 类型值 （而不转换） 并将其放入此类的任何值。 如果提供可选的第二个参数，则第一个参数的转换打包到较低的 32 位和第二个参数的转换打包到较高的 32 位。</td>
</tr>
<tr class="even">
<td align="left">namedModelParent</td>
<td align="left"><p>new namedModelParent(object, name)</p></td>
<td align="left">1</td>
<td align="left">对象的构造函数用于从返回的数组中放置<strong>initializeScript</strong>，则此表示使用 JavaScript 原型或 ES6 类作为数据模型的具有给定名称的数据模型的父扩展</td>
</tr>
<tr class="odd">
<td align="left">namedModelRegistration</td>
<td align="left"><p>新 namedModelRegistration （对象、 名称）</p></td>
<td align="left">1</td>
<td align="left">对象的构造函数用于从返回的数组中放置<strong>initializeScript</strong>，这表示 JavaScript 原型的注册或，以便可以找到其他扩展，ES6 类作为数据模型通过已知名称和扩展</td>
</tr>
<tr class="even">
<td align="left">命名空间</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">提供直接访问调试器的根命名空间。 例如，一个可以访问通过 host.namespace.Debugger.Sessions.First() 的第一个调试目标进程列表。使用此属性的进程</td>
</tr>
<tr class="odd">
<td align="left">registerNamedModel</td>
<td align="left"><p>registerNamedModel(object, modelName)</p></td>
<td align="left">2</td>
<td align="left">这将 JavaScript 原型或 ES6 类注册为在给定名称的数据模型。 此类注册允许原型或类，以定位和通过其他脚本或其他调试器扩展来扩展。 请注意，脚本应优先使用，以返回<strong>namedModelRegistration</strong>对象从其<strong>initializeScript</strong>方法，而无需执行此操作以强制方式。 以命令方式进行更改的任何脚本需要具有<strong>initializeScript</strong>方法，以清理。</td>
</tr>
<tr class="even">
<td align="left">registerExtensionForTypeSignature</td>
<td align="left"><p>registerExtensionForTypeSignature （object，typeSignature）</p></td>
<td align="left">2</td>
<td align="left">这将 JavaScript 原型或 ES6 类注册为作为给定按提供的类型签名的本机类型的扩展数据模型。 请注意，脚本应优先使用，以返回<strong>typeSignatureExtension</strong>对象从其<strong>initializeScript</strong>方法，而无需执行此操作以强制方式。 以命令方式进行更改的任何脚本需要具有<strong>initializeScript</strong>方法，以清理。</td>
</tr>
<tr class="odd">
<td align="left">registerPrototypeForTypeSignature</td>
<td align="left"><p>registerPrototypeForTypeSignature(object, typeSignature)</p></td>
<td align="left">2</td>
<td align="left">这将 JavaScript 原型或 ES6 类注册为规范化数据模型 (例如： 可视化工具) 的本机类型的指定提供的类型签名。 请注意，脚本应优先使用，以返回<strong>typeSignatureExtension</strong>对象从其<strong>initializeScript</strong>方法，而无需执行此操作以强制方式。 以命令方式进行更改的任何脚本需要具有<strong>uninitializeScript</strong>方法，以清理。</td>
</tr>
<tr class="even">
<td align="left">parseInt64</td>
<td align="left"><p>parseInt64(string, [radix])</p></td>
<td align="left">1</td>
<td align="left">此方法的标准 JavaScript parseInt 方法作用与此类似，只不过它将改为返回库 Int64 类型。 如果提供一个基数，则分析会在基本 2、 8、 10 或 16 所示。</td>
</tr>
<tr class="odd">
<td align="left">typeSignatureExtension</td>
<td align="left"><p>新 typeSignatureExtension （对象，typeSignature，[moduleName] [minVersion] [maxVersion]）</p></td>
<td align="left">1</td>
<td align="left">对象的构造函数用于从返回的数组中放置<strong>initializeScript</strong>，这表示通过 JavaScript 原型或 ES6 类通过类型签名中所述的本机类型的扩展。 此类注册&quot;将字段添加&quot;调试器到&#39;的任何类型相匹配的签名，而不是完全接管 s 可视化效果。 可选的模块名称和版本可以限制注册。 版本指定为&quot;1.2.3.4&quot;设置样式字符串。</td>
</tr>
<tr class="even">
<td align="left">typeSignatureRegistration</td>
<td align="left"><p>新 typeSignatureRegistration （对象，typeSignature，[moduleName] [minVersion] [maxVersion]）</p></td>
<td align="left">1</td>
<td align="left">对象的构造函数用于从返回的数组中放置<strong>initializeScript</strong>，这表示 JavaScript 原型或针对本机类型签名的 ES6 类的一个规范注册。 此类注册&quot;接管&quot;调试器&#39;s 可视化效果的任何类型的签名匹配，而不是只是比其进行扩展。 可选的模块名称和版本可以限制注册。 版本指定为&quot;1.2.3.4&quot;设置样式字符串。</td>
</tr>
<tr class="odd">
<td align="left">unregisterNamedModel</td>
<td align="left"><p>unregisterNamedModel(modelName)</p></td>
<td align="left">2</td>
<td align="left">这注销撤消由执行任何操作具有给定名称的数据模型从查找<strong>registerNamedModel</strong></td>
</tr>
<tr class="even">
<td align="left">unregisterExtensionForTypeSignature</td>
<td align="left"><p>unregisterExtensionForTypeSignature(object, typeSignature, [moduleName], [minVersion], [maxVersion])</p></td>
<td align="left">2</td>
<td align="left">此取消注册 JavaScript 原型或 ES6 类成为用于为给定提供的类型签名的本机类型的扩展数据模型。 RegisterExtensionForTypeSignature 逻辑撤消它。 请注意，脚本应优先使用，以返回<strong>typeSignatureExtension</strong>对象从其<strong>initializeScript</strong>方法，而无需执行此操作以强制方式。 以命令方式进行更改的任何脚本需要具有<strong>initializeScript</strong>方法，以清理。 可选的模块名称和版本可以限制注册。 版本指定为&quot;1.2.3.4&quot;设置样式字符串。</td>
</tr>
<tr class="odd">
<td align="left">unregisterPrototypeForTypeSignature</td>
<td align="left"><p>unregisterPrototypeForTypeSignature(object, typeSignature, [moduleName], [minVersion], [maxVersion])</p></td>
<td align="left">2</td>
<td align="left">此注销 JavaScript 原型或 ES6 类成为规范化数据模型 (例如： 可视化工具) 的本机类型的指定提供的类型签名。 RegisterPrototypeForTypeSignature 逻辑撤消它。 请注意，脚本应优先使用，以返回<strong>typeSignatureRegistration</strong>对象从其<strong>initializeScript</strong>方法，而无需执行此操作以强制方式。 以命令方式进行更改的任何脚本需要具有<strong>uninitializeScript</strong>方法，以清理。 可选的模块名称和版本可以限制注册。 版本指定为&quot;1.2.3.4&quot;设置样式字符串。</td>
</tr>
</tbody>
</table>

 

**诊断功能**

诊断子命名空间的该主机对象包含以下内容。

| 名称     | 签名           | 阶段存在 | 描述                                                                                                                                                                                                                                                                                                                                                   |
|----------|---------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| debugLog | debugLog(object...) | 1             | 这提供了对脚本扩展的 printf 样式调试。 目前，debugLog 输出被传送到调试器的输出控制台。 在一个更高版本的时间点，没有计划以路由此输出提供灵活性。 注意：这应不能作为一种打印用户输出到控制台。 它可能不会路由存在将来。 |

 

**内存功能**

内存子命名空间的该主机对象包含以下内容。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名称</th>
<th align="left">签名</th>
<th align="left">阶段存在</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">readMemoryValues</td>
<td align="left"><p>readMemoryValues(location, numElements, [elementSize], [isSigned], [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">它会从调试目标的地址空间读取值的原始数组并将基于此内存的视图的类型化的数组。 提供的位置可以是一个地址 （64 位值）、 位置对象或本机指针。 数组的大小将由<em>numElements</em>参数。 数组的每个元素的大小 （和类型） 提供的可选<em>elementSize</em>并<em>isSigned</em>参数。 如果未不提供任何此类参数，默认值是字节 (无符号 / 1 个字节)。 如果可选<em>contextInheritor</em>提供了参数，将在上下文中读取内存 (例如： 地址空间和调试目标) 指示参数; 否则为它将读取从调试器&#39;s 当前上下文。 请注意，上 8、 16 和 32 位值相对于放置在读取内存的快速类型化视图使用此方法。 64 位值上使用此方法会导致正在构造的 64 位库类型的数组是贵很多 ！</td>
</tr>
<tr class="even">
<td align="left">readString</td>
<td align="left"><p>readString(location, [contextInheritor])</p>
<p>readString(location, [length], [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">它会从调试目标，地址空间读取窄 （当前代码页） 字符串将其转换为 utf-16，并返回 JavaScript 字符串形式的结果。 如果无法读取内存，它可能会引发异常。 提供的位置可以是一个地址 （64 位值）、 位置对象或本机 char<em>。 如果可选<em>contextInheritor</em>提供了参数，将在上下文中读取内存 (例如： 地址空间和调试目标) 指示参数; 否则为它将读取从调试器&#39;s 当前上下文。 如果可选<em>长度</em>提供自变量，读取的字符串将为指定长度。</td>
</tr>
<tr class="odd">
<td align="left">readWideString</td>
<td align="left"><p>readWideString(location, [contextInheritor])</p>
<p>readWideString(location, [length], [contextInheritor])</p></td>
<td align="left">2</td>
<td align="left">它会从调试目标的地址空间读取 wide(UTF-16) 字符串并返回 JavaScript 字符串形式的结果。 如果无法读取内存，它可能会引发异常。 提供的位置可以是一个地址 （64 位值）、 位置对象或本机 wchar_t</em>。 如果可选<em>contextInheritor</em>提供了参数，将在上下文中读取内存 (例如： 地址空间和调试目标) 指示参数; 否则为它将读取从调试器&#39;s 当前上下文。 如果可选<em>长度</em>提供自变量，读取的字符串将为指定长度。</td>
</tr>
</tbody>
</table>

 

## <a name="span-iddata-modelspanspan-iddata-modelspanspan-iddata-modelspandata-model-concepts-in-javascript"></a><span id="Data-Model"></span><span id="data-model"></span><span id="DATA-MODEL"></span>在 JavaScript 中的数据模型概念


**数据模型映射**

以下数据模型概念可映射到 JavaScript。

| 概念                 | 本机接口             | JavaScript 等效项                                                |
|-------------------------|------------------------------|----------------------------------------------------------------------|
| 字符串转换       | IStringDisplayableConcept    | 标准： toString(...){...}                                         |
| Iterability             | IIterableConcept             | 标准版：\[Symbol.iterator\](){...}                                 |
| 可索引性            | IIndexableConcept            | 协议： getDimensionality(...) / getValueAt(...) / setValueAt(...) |
| 运行时类型转换 | IPreferredRuntimeTypeConcept | protocol: getPreferredRuntimeTypedObject(...)                        |

 

**字符串转换**

字符串转换概念 (IStringDisplayableConcept) 直接转换为标准 JavaScript **toString**方法。 因为所有 JavaScript 对象的字符串转换 （提供的 Object.prototype 如果未提供其他位置），返回到数据模型的每个 JavaScript 对象可转换为显示字符串。 重写字符串转换，只需实现你自己的 toString。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IStringDisplayableConcept::ToDisplayString(...)
    //
    toString()
    { 
        return "This is my own string conversion!";
    }
}
```

**Iterability**

一个对象是否是可迭代的或不直接映射到一个对象是否可迭代的 ES6 协议的数据模型的概念。 具有任何对象\[Symbol.iterator\]方法被视为可迭代。 此类的实现将可迭代对象。

这只是可迭代对象可以具有如下所示的实现。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        yield "First Value";
        yield "Second Value";
        yield "Third Value";
    }
}
```

特殊还必须考虑的是可迭代和可编制索引，如从迭代器返回的对象必须包含索引，以及通过特殊的返回类型的值的对象。

**可迭代并可编制索引**

是可迭代并可编制索引的对象需要一个特殊的返回值从迭代器。 而不是生成值，迭代器产生 indexedValue 的实例。 索引作为第二个参数中的数组传递给 indexedValue 构造函数。 它们可以是多维度，但必须与返回索引器协议中的维数相匹配。

此代码显示了示例 implementaion。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        //
        // Consider this a map which mapped 42->"First Value", 99->"Second Value", and 107->"Third Value"
        //
        yield new host.indexedValue("First Value", [42]);
        yield new host.indexedValue("Second Value", [99]);
        yield new host.indexedValue("Third Value", [107]);
    }
}
```

**可索引性**

与 JavaScript 不同，数据模型可使属性访问和索引之间非常明确区分。 希望各自呈现为可编制索引的数据模型中的任何 JavaScript 对象必须实现一种协议包含一个 getDimensionality 方法，它返回的索引器和 getValueAt 和 setValueAt 方法的可选对维度的执行读取和写入提供的索引处的对象。 如果对象是只读的还是只写忽略 getValueAt 或 setValueAt 方法可接受

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIndexableConcept::GetDimensionality or IIterableConcept::GetDefaultIndexDimensionality
    //
    getDimensionality()
    {
        //
        // Pretend we are a two dimensional array.
        //
        return 2;
    } 

    //
    // This method will be called whenever any native code calls IIndexableConcept::GetAt
    //
    getValueAt(row, column)
    {
        return this.__values[row * this.__columnCount + column];
    }

    //
    // This method will be called whenever any native code calls IIndexableConcept::SetAt
    //
    setValueAt(value, row, column)
    {
        this.__values[row * this.__columnCount + column] = value;
    }
}
```

**运行时类型转换**

这是仅适用于 JavaScript 原型/类针对类型系统 （本机） 类型注册。 调试器通常是能够执行分析 (例如运行时类型信息 (RTTI) / v 表分析) 来确定在代码中表示的静态类型中的对象，则返回 true 的运行时类型。 针对本机类型注册的数据模型可以重写此行为通过 IPreferredRuntimeTypeConcept 的实现。 同样，JavaScript 类或注册对本机对象的原型可以提供其自己的实现通过协议包含 getPreferredRuntimeTypedObject 方法的实现。

请注意，虽然此方法从技术上讲可以返回任何内容，它被视为错误形式，以便返回某些内容并不是真正的运行时类型或派生的类型。 此类可能会导致大量用户感到困惑的调试器。 重写此方法，但是，是非常有用的 C 样式标头 + 实现等对象样式等...

```javascript
class myNativeModel
{
    //
    // This method will be called whenever the data model calls IPreferredRuntimeTypeConcept::CastToPreferredRuntimeType
    //
    getPreferredRuntimeTypedObject()
    {
        var loc = this.targetLocation;

        //
        // Perform analysis...
        //
        var runtimeLoc = loc.Add(runtimeObjectOffset);
  
        return host.createTypedObject(runtimeLoc, runtimeModule, runtimeTypeName);
    }
}
```

## <a name="span-iddesign-considerationsspanspan-iddesign-considerationsspanspan-iddesign-considerationsspandebugger-data-model-design-considerations"></a><span id="Design-Considerations"></span><span id="design-considerations"></span><span id="DESIGN-CONSIDERATIONS"></span>调试器数据模型设计注意事项


**设计原则**

请考虑以下原则以使调试器扩展提供易于查找，可查询，并可编写脚本的信息。

-   信息是靠近需要它的位置。 例如，注册表项的信息应显示为包含注册表项句柄的本地变量的一部分。
-   信息的结构。 例如，有关注册表项的信息会显示在单独的字段，例如密钥类型、 键 ACL、 密钥名称和值。 这意味着，无需分析文本都可访问的每个字段。
-   信息是一致的。 有关注册表密钥句柄的信息所示类似的方法尽可能有关的文件句柄的信息。

避免这些方法不支持这些原则。

-   不设计您的项目结构到单个平面"厨房接收器"。 组织的层次结构，用户可以浏览它们正在寻找无需事先了解它们正在寻找的内容和支持可发现性的信息。
-   不只是仍将输出的原始文本的屏幕时将其移至该模型会转换经典 dbgeng 扩展。 这不是可组合与其他扩展，不能使用 LINQ 表达式查询。 而是将数据拆分为单独的、 可查询字段。

**命名准则**

-   字段的大小写应为 PascalCase。 异常可能被视为在另一个大小写，例如 jQuery 中广为人知的名称。
-   避免使用不通常使用 c + + 标识符中的特殊字符。 例如，避免使用"总长度"（其中包含一个空格），如名称或"\[大小\]"（包含方括号）。 此约定允许更便于使用的脚本语言，其中这些字符不允许作为标识符的一部分，并且还允许从命令窗口更便于使用。

**组织和层次结构准则**

-   不扩展调试器命名空间的最高级别。 相反，你应扩展在调试器中的现有节点，以便显示的信息是最相关。
-   不复制概念。 如果要创建列出其他信息在调试器中已存在一个概念数据模型扩展，扩展的现有信息，而不尝试将它替换为新的信息。 换而言之，将显示有关模块的详细信息的扩展应扩展的现有*模块*对象而不是创建新的模块列表。
-   免费浮点实用程序的命令必须属于*Debugger.Utility*命名空间。 它们还应适当地为子命名空间 (例如*Debugger.Utility.Collections.FromListEntry*)

**向后兼容性和重大更改**

发布的脚本应该不会中断与其他脚本依赖于它的兼容性。 例如，如果一个函数发布到该模型，它应保留相同的位置，并且使用相同的参数，只要有可能。

**不使用的外部资源**

-   扩展必须生成外部进程。 外部进程可能会干扰调试器的行为，并在各种远程调试器的情况下 （例如 dbgsrv 远程存储库、 ntsd 远程存储库和"ntsd-d 远程"） 将出现异常行为
-   扩展必须不显示任何用户界面。 显示用户界面元素上远程调试的情况下，将不正确的行为，并可能会中断调试方案的控制台。
-   扩展中不能处理调试器引擎或调试器用户界面通过未记录的方法。 这会导致兼容性问题，并使用不同的 UI 的调试器客户端上的正确行为。
-   扩展必须仅通过有案可稽的调试器 Api 访问目标信息。 尝试通过 win32 Api 将失败的许多远程方案中，并甚至一些本地调试方案，跨安全边界访问有关目标的信息。

**不使用的 Dbgeng 特定的功能**

旨在用作扩展的脚本必须不依赖于特定于 dbgeng 的功能，只要有可能 （例如在执行"经典"调试器扩展）。 脚本应该可以使用任何调试器承载的数据模型之上。

## <a name="span-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspantesting-debugger-extensions"></a><span id="Testing-Debugger-Extensions"></span><span id="testing-debugger-extensions"></span><span id="TESTING-DEBUGGER-EXTENSIONS"></span>测试调试器扩展


扩展应在范围广泛的方案中工作。 尽管某些扩展可能是特定于方案 （如内核调试方案中），应期望大多数扩展能够使用在所有情况下，或者遇到元数据，该值指示支持的方案。

内核模式

-   实时内核调试
-   内核转储调试

用户模式

-   实时用户模式下调试
-   用户模式转储调试

此外，请考虑这些调试器使用方案

-   多进程调试
-   调试 （例如转储 + 单个会话中的实时用户） 的多会话

**远程调试器使用情况**

测试与远程调试器使用方案的正确操作。

-   dbgsrv 远程存储库
-   ntsd 远程存储库
-   ntsd-d 的远程存储库

有关详细信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)并[**激活进程服务器**](activating-a-process-server.md)。

**回归测试**

调试器的新版本的发布，请调查可以验证你的扩展功能的测试自动化的使用。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[脚本编写的 JavaScript 调试器](javascript-debugger-scripting.md)

[JavaScript 调试器的示例脚本](javascript-debugger-example-scripts.md)

 

 






