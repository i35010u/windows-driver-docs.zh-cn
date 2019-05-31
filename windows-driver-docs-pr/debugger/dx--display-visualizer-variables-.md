---
title: dx（显示调试器对象模型表达式）
description: Dx 命令显示C++表达式中使用 NatVis 扩展模型。 Dx 命令处理调试器对象。
ms.assetid: 93047911-5195-4FB9-A015-5349084EDC0A
keywords:
- dx （显示调试器对象模型表达式） Windows 调试
ms.date: 05/28/2019
topic_type:
- apiref
api_name:
- dx (Display Debugger Object Model Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 65d63e3469b6e18f58eebcbbe245f81364156828
ms.sourcegitcommit: e123b8b69473c0ebc0383ef722452866bf6662d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66394279"
---
# <a name="dx-display-debugger-object-model-expression"></a>dx（显示调试器对象模型表达式）


**Dx**命令将显示C++使用 NatVis 扩展模型表达式。 NatVis 有关详细信息，请参阅[创建本机对象的自定义视图](https://msdn.microsoft.com/library/jj620914.aspx)。

```dbgcmd
dx [-g|-gc #][-c #][-n|-v]-r[#] Expression[,<FormatSpecifier> ]
dx [{-?}|{-h}]
```

## <a name="span-idddkcmddisplaytypedbgspanspan-idddkcmddisplaytypedbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
一个C++要显示的表达式。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
显示为数据网格对象，后者是可迭代。 每个循环访问元素是在网格中的行并且这些元素的每个显示子列。 这样，您可以查看类似于数组的结构，其中每个数组元素显示在一行中和结构的每个字段显示在列中。

保持单击列名称 （如果没有可用的 DML 链接） 将按该列排序。 如果已按该列排序，则将反转排序顺序。

这是可迭代的任何对象将具有项已添加名为显示为网格 DML 通过右键单击上下文菜单。 右键单击输出窗口中的对象，然后选择此项将显示在网格视图中而不是标准树视图的对象。

（+） 显示的列命名产品/服务这两个右键单击和左键单击行为。

-   左键的单击采用该列，并解压后生成它自己的表。 您会看到原始行以及扩展的列的子级。
-   右键单击提供"展开到网格"采用列并将其返回到当前表添加为正确的大多数列。

<span id="_______-gc________"></span><span id="_______-GC________"></span> **-gc \#**    
显示为一个网格，并将网格单元格的大小限制为指定的数 (\#) 字符。

<span id="_______-c________"></span><span id="_______-C________"></span> **-c \#**    
显示容器延续 (跳过\#容器中的元素)。此选项通常用于自定义输出自动化方案，并提供一个"..."在列表底部的继续符元素。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
有两种方法可呈现数据。 使用 NatVis 可视化效果 （默认值） 或使用基础本机 C /C++结构。 指定要呈现的输出使用只是本机的 C-n 参数 /C++结构和不 NatVis 可视化效果。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示详细信息，包括方法和其他非典型的对象。

<span id="_______-r_______"></span><span id="_______-R_______"></span> **-r**<em>\#</em>   
以递归方式显示子 （字段） 最多 *\#* 级别。 如果 *\#* 是未指定，1，递归级别是默认值。

<span id="__________FormatSpecifier_________"></span><span id="__________formatspecifier_________"></span><span id="__________FORMATSPECIFIER_________"></span> **\[&lt;,FormatSpecifier&gt;\]**    
使用任何下列格式说明符来修改默认的呈现。

|                         |                                                                                          |
|-------------------------|------------------------------------------------------------------------------------------|
| x                      | 在十六进制显示序号                                                          |
| d                      | 以十进制显示序号                                                              |
| o                      | 在八进制中显示序号                                                                |
| ,b                      | 显示二进制文件中的序号                                                               |
| en                     | 通过仅名称 （没有值） 显示枚举                                                    |
| ,c                      | 显示为单个字符 （而不是字符串）                                               |
| s                      | 显示 8 位字符串，如带引号的 ASCII                                                    |
| ,sb                     | 显示为不带引号的 ASCII 8 位字符串                                                  |
| ,s8                     | 显示 8 位字符串，如带引号的 utf-8                                                    |
| ,s8b                    | 显示为 utf-8 不带引号的 8 位字符串                                                  |
| ,su                     | 显示 16 位字符串，如带引号的 utf-16                                                  |
| ,sub                    | 显示为 utf-16 unqouted 的 16 位字符串                                                |
| ,!                      | 只在 raw 模式中显示对象 (例如： 没有 NatVis)                                       |
| ,\#                     | 作为文本值指定长度的指针/数组/容器\#（使用数字替换） |
| ,\[&lt;expression&gt;\] | 指定作为表达式的长度的指针/数组/容器&lt;表达式&gt;           |
| nd                     | 不到对象的派生 (runtype) 类型。 仅显示静态值          |

<span id="_______dx_-_______"></span><span id="_______DX_-_______"></span> **dx** { **-?** }   
显示命令行帮助。

<span id="_______dx_-h______"></span><span id="_______DX_-H______"></span> **dx** { **-h**}   
显示可在调试器中的对象的帮助。

<span id="_______dx_-id______"></span><span id="_______DX_-ID______"></span> **dx** { **-id**}   
仅限 Microsoft 内部使用。 用于跟踪命令输出中的数据模型链接。

## <a name="command-line-usage-example"></a>命令行用法示例

.Dx 设置命令可以用于显示有关调试设置对象的信息。 有关调试设置对象的详细信息，请参阅[ **.settings** ](-settings--set-debug-settings-.md) 。
```dbgcmd
kd> dx -r1 Debugger.Settings
Debugger.Settings : 
    Display          : 
    EngineInitialization : 
    Extensions       : 
    Input            : 
    Sources          : 
    Symbols          : 
    AutoSaveSettings : false
```

使用-r1 递归选项以查看其他调试器对象-会话、 设置和状态。

```dbgcmd
kd> dx -r1 Debugger
Debugger : 
  Sessions : 
  Settings : 
  State    : 
```

指定 Debugger.Sessions 旅行的-r3 递归选项对象随后将向下的对象链。

```dbgcmd
kd> dx -r3 Debugger.Sessions
Debugger.Sessions : 
  [0]              : Remote KD: KdSrv:Server=@{<Local>},Trans=@{1394:Channel=0}
    Processes : 
      [0]              : <Unknown Image>
      [4]              : <Unknown Image>
      [304]            : smss.exe
      [388]            : csrss.exe
      [456]            : wininit.exe
      [468]            : csrss.exe
      [528]            : services.exe
      [536]            : lsass.exe
      [544]            : winlogon.exe
      [620]            : svchost.exe
       ...               ...
```

添加 x 格式说明符，以十六进制格式显示的顺序值。

```dbgcmd
kd> dx -r3 Debugger.Sessions,x
Debugger.Sessions,x : 
  [0x0]            : Remote KD: KdSrv:Server=@{<Local>},Trans=@{1394:Channel=0}
    Processes : 
      [0x0]            : <Unknown Image>
      [0x4]            : <Unknown Image>
      [0x130]          : smss.exe
      [0x184]          : csrss.exe
      [0x1c8]          : wininit.exe
      [0x1d4]          : csrss.exe
      [0x210]          : services.exe
      [0x218]          : lsass.exe
      [0x220]          : winlogon.exe
      [0x26c]          : svchost.exe
      [0x298]          : svchost.exe
      [0x308]          : dwm.exe
      [0x34c]          : nvvsvc.exe
      [0x37c]          : nvvsvc.exe
      [0x384]          : svchost.exe
       ...               ...
```

此示例使用活动的调试会话列表中第一个过程的第一个线程的调用堆栈。

```dbgcmd
kd> dx -r1 Debugger.Sessions.First().Processes.First().Threads.First().Stack.Frames
Debugger.Sessions.First().Processes.First().Threads.First().Stack.Frames : 
    [0x0]            : nt!RtlpBreakWithStatusInstruction
    [0x1]            : nt!KdCheckForDebugBreak + 0x7a006
    [0x2]            : nt!KiUpdateRunTime + 0x42
    [0x3]            : nt!KiUpdateTime + 0x129
    [0x4]            : nt!KeClockInterruptNotify + 0x1c3
    [0x5]            : hal!HalpTimerClockInterruptEpilogCommon + 0xa
    [0x6]            : hal!HalpTimerClockInterruptCommon + 0x3e
    [0x7]            : hal!HalpTimerClockInterrupt + 0x1cb
    [0x8]            : nt!KiIdleLoop + 0x1a
```

-G 选项用于为数据网格中显示输出。 单击要排序的列。

```dbgcmd
kd> dx -g @$curprocess.Modules
```

![output from dx -g @$curprocess.modules showing columnar grid output](images/dx-grid-example.png)

使用-h 选项可显示有关对象的信息。
```dbgcmd
kd>  dx -h Debugger.State
Debugger.State   [State pertaining to the current execution of the debugger (e.g.: user variables)]
    DebuggerVariables [Debugger variables which are owned by the debugger and can be referenced by a pseudo-register prefix of @$]
    PseudoRegisters   [Categorizied debugger managed pseudo-registers which can be referenced by a pseudo-register prefix of @$]
    UserVariables     [User variables which are maintained by the debugger and can be referenced by a pseudo-register prefix of @$]
```

## <a name="displaying-teb-and-peb-information-using-the-environment-object"></a>显示 TEB 和 PEB 信息使用环境对象

使用环境对象来显示 TEB 和 PEB 信息与线程和进程相关联。

若要显示 TEB 关联与当前线程使用此命令。

```dbgcmd
0: kd> dx -r2 @$curthread.Environment
@$curthread.Environment                
    EnvironmentBlock [Type: _TEB]
        [+0x000] NtTib            [Type: _NT_TIB]
        [+0x038] EnvironmentPointer : Unable to read memory at Address 0x38
        [+0x040] ClientId         [Type: _CLIENT_ID]
        [+0x050] ActiveRpcHandle  : Unable to read memory at Address 0x50
        [+0x058] ThreadLocalStoragePointer : Unable to read memory at Address 0x58
        [+0x060] ProcessEnvironmentBlock : Unable to read memory at Address 0x60
        [+0x068] LastErrorValue   : Unable to read memory at Address 0x68
        [+0x06c] CountOfOwnedCriticalSections : Unable to read memory at Address 0x6c
        [+0x070] CsrClientThread  : Unable to read memory at Address 0x70
        [+0x078] Win32ThreadInfo  : Unable to read memory at Address 0x78
        [+0x080] User32Reserved   [Type: unsigned long [26]]
        [+0x0e8] UserReserved     [Type: unsigned long [5]]
        [+0x100] WOW32Reserved    : Unable to read memory at Address 0x100
        [+0x108] CurrentLocale    : Unable to read memory at Address 0x108
        [+0x10c] FpSoftwareStatusRegister : Unable to read memory at Address 0x10c
         ...
```

若要显示 PEB 关联进程当前使用此命令。

```dbgcmd
0: kd> dx -r2 @$curprocess.Environment
@$curprocess.Environment                
    EnvironmentBlock [Type: _PEB]
        [+0x000] InheritedAddressSpace : Unable to read memory at Address 0x0
        [+0x001] ReadImageFileExecOptions : Unable to read memory at Address 0x1
        [+0x002] BeingDebugged    : Unable to read memory at Address 0x2
        [+0x003] BitField         : Unable to read memory at Address 0x3
        [+0x003 ( 0: 0)] ImageUsesLargePages : Unable to read memory at Address 0x3
        [+0x003 ( 1: 1)] IsProtectedProcess : Unable to read memory at Address 0x3
        [+0x003 ( 2: 2)] IsImageDynamicallyRelocated : Unable to read memory at Address 0x3
        [+0x003 ( 3: 3)] SkipPatchingUser32Forwarders : Unable to read memory at Address 0x3
        [+0x003 ( 4: 4)] IsPackagedProcess : Unable to read memory at Address 0x3
        [+0x003 ( 5: 5)] IsAppContainer   : Unable to read memory at Address 0x3
        [+0x003 ( 6: 6)] IsProtectedProcessLight : Unable to read memory at Address 0x3
        [+0x003 ( 7: 7)] IsLongPathAwareProcess : Unable to read memory at Address 0x3
        [+0x004] Padding0         [Type: unsigned char [4]]
        [+0x008] Mutant           : Unable to read memory at Address 0x8
        [+0x010] ImageBaseAddress : Unable to read memory at Address 0x10
        [+0x018] Ldr              : Unable to read memory at Address 0x18
        [+0x020] ProcessParameters : Unable to read memory at Address 0x20
        ...
```


## <a name="kernel-iohandles-object"></a>内核 Io.Handles 对象

使用当前进程 Io.Handles 对象显示内核句柄的信息。

```dbgcmd
0: kd> dx -r1 @$curprocess.Io.Handles
@$curprocess.Io.Handles                
    [0x8]           
    [0xc]           
    [0x10]          
    [0x14]          
    [0x18]       
    ...
```

使用。First （） 函数来显示有关第一个句柄的信息。

```dbgcmd
0: kd> dx -r2 @$curprocess.Io.Handles.First()
@$curprocess.Io.Handles.First()                
    Handle           : 0x8
    Type             : Unexpected failure to dereference object
    GrantedAccess    : Unexpected failure to dereference object
    Object           [Type: _OBJECT_HEADER]
        [+0x000] PointerCount     : 228806 [Type: __int64]
        [+0x008] HandleCount      : 6 [Type: __int64]
        [+0x008] NextToFree       : 0x6 [Type: void *]
        [+0x010] Lock             [Type: _EX_PUSH_LOCK]
        [+0x018] TypeIndex        : 0xf2 [Type: unsigned char]
        [+0x019] TraceFlags       : 0x0 [Type: unsigned char]
        [+0x019 ( 0: 0)] DbgRefTrace      : 0x0 [Type: unsigned char]
        [+0x019 ( 1: 1)] DbgTracePermanent : 0x0 [Type: unsigned char]
        [+0x01a] InfoMask         : 0x0 [Type: unsigned char]
        [+0x01b] Flags            : 0x2 [Type: unsigned char]
        [+0x01b ( 0: 0)] NewObject        : 0x0 [Type: unsigned char]
        [+0x01b ( 1: 1)] KernelObject     : 0x1 [Type: unsigned char]
        [+0x01b ( 2: 2)] KernelOnlyAccess : 0x0 [Type: unsigned char]
        [+0x01b ( 3: 3)] ExclusiveObject  : 0x0 [Type: unsigned char]
        [+0x01b ( 4: 4)] PermanentObject  : 0x0 [Type: unsigned char]
        [+0x01b ( 5: 5)] DefaultSecurityQuota : 0x0 [Type: unsigned char]
        [+0x01b ( 6: 6)] SingleHandleEntry : 0x0 [Type: unsigned char]
        [+0x01b ( 7: 7)] DeletedInline    : 0x0 [Type: unsigned char]
        [+0x01c] Reserved         : 0x0 [Type: unsigned long]
        [+0x020] ObjectCreateInfo : 0xfffff801f6d9c6c0 [Type: _OBJECT_CREATE_INFORMATION *]
        [+0x020] QuotaBlockCharged : 0xfffff801f6d9c6c0 [Type: void *]
        [+0x028] SecurityDescriptor : 0xffffb984aa815d06 [Type: void *]
        [+0x030] Body             [Type: _QUAD]
        ObjectType       : Unexpected failure to dereference object
        UnderlyingObject : Unexpected failure to dereference object
```

请注意，Io.Handles 对象内核唯一对象。


## <a name="working-around-symbol-file-limitations-with-casting"></a>解决与强制转换的符号文件限制

在显示有关各种 Windows 系统变量的信息时，有些时候，并非所有类型信息现已推出公共符号。 此示例说明了这种情况。

```dbgcmd
0: kd> dx nt!PsIdleProcess
Error: No type (or void) for object at Address 0xfffff800e1d50128
```

Dx 命令支持的功能，以引用不具有类型信息的变量的地址。 此类"的地址"的引用将被视为"void \*"，并且可以这种情况下强制转换。 这意味着，如果数据类型已知时，可以使用以下语法来显示变量的类型信息。

```dbgcmd
dx (Datatype *)&VariableName
```

例如对于 nt ！数据类型为 nt 的 PsIdleProcess ！\_EPROCESS，使用此命令。

```dbgcmd
dx (nt!_EPROCESS *)&nt!PsIdleProcess
(nt!_EPROCESS *)&nt!PsIdleProcess                 : 0xfffff800e1d50128 [Type: _EPROCESS *]
    [+0x000] Pcb              [Type: _KPROCESS]
    [+0x2c8] ProcessLock      [Type: _EX_PUSH_LOCK]
    [+0x2d0] CreateTime       : {4160749568} [Type: _LARGE_INTEGER]
    [+0x2d8] RundownProtect   [Type: _EX_RUNDOWN_REF]
    [+0x2e0] UniqueProcessId  : 0x1000 [Type: void *]
    [+0x2e8] ActiveProcessLinks [Type: _LIST_ENTRY]
    [+0x2f8] Flags2           : 0x218230 [Type: unsigned long]
    [+0x2f8 ( 0: 0)] JobNotReallyActive : 0x0 [Type: unsigned long]
```

Dx 命令不支持切换表达式计算器使用 @ @ MASM 语法。 有关表达式计算器的详细信息，请参阅[评估表达式](evaluating-expressions.md)。

## <a name="using-linq-with-the-debugger-objects"></a>将 LINQ 与调试器对象配合使用

可以使用调试器对象使用 LINQ 语法，用于搜索和操作数据。 LINQ 是从概念上讲类似到结构化查询语言 (SQL)，用于查询数据库。 许多 LINQ 方法可用于搜索、 筛选和分析调试数据。 了解我们使用 LINQ 和对象的调试器，请参阅[使用调试器对象与 LINQ](using-linq-with-the-debugger-objects.md)。

## <a name="using-debugger-objects-with-natvis-and-javascript"></a>使用 NatVis 和 JavaScript 使用调试器对象

使用 NatVis 调试器对象有关的信息，请参阅[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)。

与 JavaScript 一起使用调试器对象的信息，请参阅[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅

[使用 LINQ 与调试器对象](using-linq-with-the-debugger-objects.md)

[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)

[中 JavaScript 扩展本机调试器对象](native-objects-in-javascript-extensions.md) 

---







