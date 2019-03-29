---
title: wt（跟踪和监视数据）
description: Wt 命令在整个函数中运行，，然后显示统计信息时执行此命令在函数调用的开始。
ms.assetid: 2dd62a7f-67d9-4b13-b04e-5cd02e6ef9f0
keywords:
- wt （跟踪和查看数据） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wt (Trace and Watch Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8208441e26b826ae15708fdff3621eb4c25ab14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563834"
---
# <a name="wt-trace-and-watch-data"></a>wt（跟踪和监视数据）


**Wt**命令在整个函数中运行，然后显示统计信息，，在执行此命令在函数调用的开始。

```dbgcmd
wt [WatchOptions] [= StartAddress] [EndAddress] 
```

## <a name="span-idddkcmdtraceandwatchdatadbgspanspan-idddkcmdtraceandwatchdatadbgspanparameters"></a><span id="ddk_cmd_trace_and_watch_data_dbg"></span><span id="DDK_CMD_TRACE_AND_WATCH_DATA_DBG"></span>参数


<span id="_______WatchOptions______"></span><span id="_______watchoptions______"></span><span id="_______WATCHOPTIONS______"></span> *WatchOptions*   
指定如何修改显示。 您可以使用任何以下选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-l</strong> <em>Depth</em></p></td>
<td align="left"><p>（仅限用户模式）指定要显示的调用的最大深度。 至少为任何调用<em>深度</em>级别更深层次的起始点比以无提示方式执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong> <em>模块</em></p></td>
<td align="left"><p>（仅限用户模式）将显示限制为指定的模块，以及从该模块进行的调用的第一个级别内的代码。 可以包含多个-m 选项以显示来自多个模块和任何其他模块的代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-i</strong> <em>模块</em></p></td>
<td align="left"><p>（仅限用户模式）将忽略指定模块内的任何代码。 可以包含多个-i 选项忽略从多个模块的代码。 如果使用-m 选项，调试器会忽略所有-i 选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ni</strong></p></td>
<td align="left"><p>（仅限用户模式）不会显示为-m 忽略的代码中的任何条目或-i 选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-nc</strong></p></td>
<td align="left"><p>不显示各个调用信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ns</strong></p></td>
<td align="left"><p>不显示摘要信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-nw</strong></p></td>
<td align="left"><p>在跟踪期间将不显示警告。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-oa</strong></p></td>
<td align="left"><p>（仅限用户模式）显示调用站点的实际地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-or</strong></p></td>
<td align="left"><p>（仅限用户模式）显示被调用函数，使用默认基数为基础的返回的注册值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-oR</strong></p></td>
<td align="left"><p>（仅限用户模式）显示被调用函数，为每个相应的类型中返回的注册值返回值。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定调试器开始执行的位置的地址。 如果不使用*StartAddress*，指令指针指向的指令处开始执行。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______EndAddress______"></span><span id="_______endaddress______"></span><span id="_______ENDADDRESS______"></span> *EndAddress*   
指定跟踪的结束位置的地址。 如果不使用*EndAddress*，执行一次的指令或函数调用。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p></p>
<strong>用户模式下：</strong>所有<strong>内核模式：</strong>基于 x86 的仅</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

详细了解颁发**wt**相关命令的命令和的概述，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Wt**命令很有用，如果您希望的行为信息的特定函数，但您不想要单步执行函数。 相反，请转到该函数的开头，然后发出**wt**命令。

如果程序计数器是对应于符号 （如到模块中函数或入口点开始），某时刻**wt**命令跟踪，直到它达到当前寄信人地址。 如果程序计数器位于**调用**指令**wt**命令跟踪，直到它返回到当前的位置。 在分析此跟踪[调试器命令窗口](debugger-command-window.md)以及描述该命令遇到的各种调用的输出。

如果**wt**函数的开头之外某处发出命令，该命令的行为类似于[ **p （步骤）** ](p--step-.md)命令。 但是，如果您指定*EndAddress*，执行将继续，直至达到地址，即使此执行涉及到许多步骤进行编程和函数调用。

在源模式中调试时，应该仅对将出现在函数体的左大括号的点函数中进行跟踪。 然后，可以使用**wt**命令。 (通常很容易在该函数的第一行处插入一个断点或使用[调试 |运行到光标处](debug---run-to-cursor.md)，然后使用**wt**命令。)

因为从输出**wt**可能很长，可能想要使用的日志文件来记录你的输出。

下面的示例显示了典型的日志文件。

```dbgcmd
0:000> l+                  Source options set to show source lines
Source options are f:
     1/t - Step/trace by source line
     2/l - List source line for LN and prompt
     4/s - List source code at prompt
     8/o - Only show source code at prompt
0:000> p                   Not yet at the function call: use "p"
>  44:       minorVariableOne = 12;
0:000> p
>  45:       variableOne = myFunction(2, minorVariable);
0:000> t                   At the function call: now use "t"
MyModule!ILT+10(_myFunction):
0040100f e9cce60000      jmp     MyModule!myFunction (0040f6e0)
0:000> t
>  231:    { 
0:000> wt                  At the function beginning:  now use "wt"
Tracing MyModule!myFunction to return address 00401137

  105     0 [  0] MyModule!myFunction
    1     0 [  1]   MyModule!ILT+1555(_printf)
    9     0 [  1]   MyModule!printf
    1     0 [  2]     MyModule!ILT+370(__stbuf)
   11     0 [  2]     MyModule!_stbuf
    1     0 [  3]       MyModule!ILT+1440(__isatty)
   14     0 [  3]       MyModule!_isatty
   50    15 [  2]     MyModule!_stbuf
   17    66 [  1]   MyModule!printf
    1     0 [  2]     MyModule!ILT+980(__output)
   59     0 [  2]     MyModule!_output
   39     0 [  3]       MyModule!write_char
  111    39 [  2]     MyModule!_output
   39     0 [  3]       MyModule!write_char

....

   11     0 [  5]           kernel32!__SEH_epilog4
   54 11675 [  4]         kernel32!ReadFile
  165 11729 [  3]       MyModule!_read
  100 11895 [  2]     MyModule!_filbuf
   91 11996 [  1]   MyModule!fgets
54545 83789 [  0] MyModule!myFunction
    1     0 [  1]   MyModule!ILT+1265(__RTC_CheckEsp)
    2     0 [  1]   MyModule!_RTC_CheckEsp
54547 83782 [  0] MyModule!myFunction

112379 instructions were executed in 112378 events (0 from other threads)

Function Name                               Invocations MinInst MaxInst AvgInst
MyModule!ILT+1265(__RTC_CheckEsp)                     1       1       1       1
MyModule!ILT+1440(__isatty)                          21       1       1       1
MyModule!ILT+1540(__ftbuf)                           21       1       1       1
....
ntdll!memcpy                                         24       1      40      19
ntdll!memset                                          2      29      29      29

23 system calls were executed

Calls  System Call
   23  ntdll!KiFastSystemCall
```

在跟踪的列表中，第一个数字指定的已执行的指令数，第二个数字指定由子进程的函数执行的指令数并 （在方括号中） 的第三个数字指定的深度（使用零作为初始函数） 在堆栈中的函数。 函数名称的缩进显示调用深度。

在前面的示例中， **MyModule ！ myFunction**之前它将调用多个子例程，包括执行 105 指令**printf**并**fgets**，然后执行54545 其他说明之后调用这些函数，但之前发出几个更多调用。 但是，在最终计数中，屏幕将显示该**myFunction**执行 112,379 指令，因为此计数包括的所有说明的**myFunction**和及其子级执行。 (*子级*的**myFunction**是从调用的函数**myFunction**，直接或间接。)

在前面的示例中，另请注意**ILT + 1440年 (\_\_isatty)** 称为 21 次。 在最终计数中，此函数的行为的摘要会显示它已调用的次数、 最少数量的任何单个执行中的说明、 最大数量的任何单个执行中的说明和说明的平均数每次执行。

如果进行了任何系统调用，它们显示在计数器，并再次命令输出的末尾处列出。

 

 





