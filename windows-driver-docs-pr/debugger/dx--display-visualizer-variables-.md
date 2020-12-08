---
title: dx（显示调试器对象模型表达式）
description: Dx 命令显示使用 NatVis 扩展模型的 c + + 表达式。 Dx 命令适用于调试器对象。
keywords:
- dx (显示) Windows 调试的调试器对象模型表达式
ms.date: 05/28/2019
topic_type:
- apiref
api_name:
- dx (Display Debugger Object Model Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1734913957e9df1dc2c80a25fab6bb41a6f72536
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838655"
---
# <a name="dx-display-debugger-object-model-expression"></a>dx（显示调试器对象模型表达式）


**Dx** 命令显示使用 NatVis 扩展模型的 c + + 表达式。 有关 NatVis 的详细信息，请参阅 [创建本机对象的自定义视图](/visualstudio/debugger/create-custom-views-of-native-objects)。

```dbgcmd
dx [-g|-gc #][-c #][-n|-v]-r[#] Expression[,<FormatSpecifier> ]
dx [{-?}|{-h}]
```

## <a name="span-idddk_cmd_display_type_dbgspanspan-idddk_cmd_display_type_dbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
要显示的 c + + 表达式。

<span id="_______-g______"></span><span id="_______-G______"></span>**-g**   
显示为可迭代的数据网格对象。 每个迭代元素都是网格中的一行，这些元素的每个显示子级都是一个列。 这使您可以查看结构数组，如结构数组，其中每个数组元素都显示在行中，结构的每个字段都显示在一列中。

选择一个列名称 (其中包含可用的 DML 链接) 将按该列进行排序。 如果已按该列进行排序，则将反转排序顺序。

任何可迭代的对象都具有 select 和 hold (或右键单击通过 "显示为网格" 的 DML 添加) 上下文菜单项。 选择并按住 (或右键单击 "输出" 窗口中的某个对象) 并选择此项将在网格视图中显示该对象，而不是标准树视图。

列名称显示的 (+) 既提供了选择的 (，也提供了右键单击) 和选择行为。

-   选择 "提取该列" 并将其分解为自己的表。 您将看到原始行加上展开列的子级。
-   选择并按住 (或右键单击) 提供 "扩展到网格"，它将列，并将其作为最大列添加回当前表。

<span id="_______-gc________"></span><span id="_______-GC________"></span>**-gc \#**   
显示为网格，并将网格单元大小限制为指定数量的 (\#) 字符。

<span id="_______-c________"></span><span id="_______-C________"></span>**-c \#**   
显示容器继续 (跳过 \# 容器) 的元素。此选项通常用于自定义输出自动化方案，并提供 "..."列表底部的继续符元素。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
可以通过两种方式来呈现数据。 使用 NatVis 可视化 (默认) 或使用基础本机 C/c + + 结构。 使用纯 C/c + + 结构而不是 NatVis 可视化对象指定-n 参数以呈现输出。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
显示包括方法和其他非典型对象的详细信息。

<span id="_______-r_______"></span><span id="_______-R_______"></span>**-r**<em>\#</em>   
以递归方式显示) 多个级别的子类型 (字段 *\#* 。 如果 *\#* 未指定，则递归级别为1，默认值为。

<span id="__________FormatSpecifier_________"></span><span id="__________formatspecifier_________"></span><span id="__________FORMATSPECIFIER_________"></span>**\[ &lt; ， &gt; FormatSpecifier \]**   
使用以下任意格式说明符修改默认呈现。

**，x**：以十六进制显示序号

**，d**：以十进制显示序号

**，o**：以八进制显示序号

**，b**：以二进制形式显示序号

**，en**：仅按名称显示枚举 (没有值) 

**，c**：显示为单个字符 (不是字符串) 

**，s**：将8位字符串显示为 ASCII 引号

**，sb**：将8位字符串显示为 ASCII 未加引号

**，s8**：以 utf-8 括起来显示8位字符串

**，s8b**：以 utf-8 无引号显示8位字符串

**，su**：将16位字符串显示为 utf-16 引号

**，sub**：显示16位字符串作为 utf-16 unqouted

**，！**：仅在原始模式下显示对象 (例如： no NatVis) 

**， \#**：指定指针/数组/容器的长度作为文本值 \# (替换为数值) 

**,\[&lt;&gt;expression \]**：指定指针/数组/容器的长度作为表达式 &lt; 表达式&gt;

**，nd**：找不到对象的派生 (runtype) 类型。 仅显示静态值


<span id="_______dx_-_______"></span><span id="_______DX_-_______"></span>**dx** {**-？**}   
显示命令行帮助。

<span id="_______dx_-h______"></span><span id="_______DX_-H______"></span>**dx** {**-h**}   
显示调试器中可用对象的帮助。

<span id="_______dx_-id______"></span><span id="_______DX_-ID______"></span>**dx** {**-id**}   
仅供 Microsoft 内部使用。 用于在命令输出中跟踪数据模型链接。

## <a name="command-line-usage-example"></a>命令行用法示例

可以使用 "dx 设置" 命令显示有关 "调试设置" 对象的信息。 有关调试设置对象的详细信息，请参阅 [**。**](-settings--set-debug-settings-.md)
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

使用-r1 递归选项查看其他调试器对象-会话、设置和状态。

```dbgcmd
kd> dx -r1 Debugger
Debugger : 
  Sessions : 
  Settings : 
  State    : 
```

指定带有-r3 递归选项的 "会话" 对象，以便沿对象链向下移动。

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

添加 x 格式说明符以以十六进制显示序号值。

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

此示例使用活动的调试会话来列出第一个进程中第一个线程的调用堆栈。

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

使用-g 选项将输出显示为数据网格。 选择要排序的列。

```dbgcmd
kd> dx -g @$curprocess.Modules
```

![dx-g @ $curprocess 的输出显示纵栏式网格输出](images/dx-grid-example.png)

使用-h 选项显示有关对象的信息。
```dbgcmd
kd>  dx -h Debugger.State
Debugger.State   [State pertaining to the current execution of the debugger (e.g.: user variables)]
    DebuggerVariables [Debugger variables which are owned by the debugger and can be referenced by a pseudo-register prefix of @$]
    PseudoRegisters   [Categorizied debugger managed pseudo-registers which can be referenced by a pseudo-register prefix of @$]
    UserVariables     [User variables which are maintained by the debugger and can be referenced by a pseudo-register prefix of @$]
```

## <a name="displaying-teb-and-peb-information-using-the-environment-object"></a>使用环境对象显示 TEB 和 PEB 信息

使用 "环境" 对象可显示与线程和进程关联的 TEB 和 PEB 信息。

若要显示与当前线程关联的 TEB，请使用此命令。

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

若要显示与当前进程关联的 PEB，请使用此命令。

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


## <a name="kernel-iohandles-object"></a>内核 Io。 Handles 对象

使用当前进程 Io。 Handles 对象以显示内核句柄信息。

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

使用。首先 ( # A1 函数以显示有关第一个句柄的信息。

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

请注意，"Io" 对象是 "仅限内核" 对象。


## <a name="working-around-symbol-file-limitations-with-casting"></a>使用强制转换解决符号文件限制

在显示有关各种 Windows 系统变量的信息时，有些情况下，公共符号中并没有所有类型信息可用。 此示例阐释了这种情况。

```dbgcmd
0: kd> dx nt!PsIdleProcess
Error: No type (or void) for object at Address 0xfffff800e1d50128
```

Dx 命令支持引用不包含类型信息的变量的地址。 此类 "address" 引用被视为 "void \* "，可以转换为。 这意味着，如果数据类型已知，则可以使用以下语法来显示变量的类型信息。

```dbgcmd
dx (Datatype *)&VariableName
```

例如，nt！PsIdleProcess 的数据类型为 nt！ \_EPROCESS，请使用此命令。

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

Dx 命令不支持用 @ @ MASM 语法切换表达式计算器。 有关表达式计算器的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

## <a name="using-linq-with-the-debugger-objects"></a>将 LINQ 与调试器对象配合使用

LINQ 语法可以与调试器对象结合使用来搜索和操作数据。 LINQ 在概念上类似于用于查询数据库 (SQL) 的结构化查询语言。 可以使用多个 LINQ 方法搜索、筛选和分析调试数据。 有关将 LINQ 与调试器对象结合使用的信息，请参阅 [将 Linq 与调试器对象配合使用](using-linq-with-the-debugger-objects.md)。

## <a name="using-debugger-objects-with-natvis-and-javascript"></a>将调试器对象用于 NatVis 和 JavaScript

有关将调试器对象与 NatVis 结合使用的信息，请参阅 [NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)。

有关将调试器对象与 JavaScript 一起使用的信息，请参阅 [Javascript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。


## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[将 LINQ 与调试器对象配合使用](using-linq-with-the-debugger-objects.md)

[NatVis 中的本机调试器对象](native-debugger-objects-in-natvis.md)

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md) 

---
