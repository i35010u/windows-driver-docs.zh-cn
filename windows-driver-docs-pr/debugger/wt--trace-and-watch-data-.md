---
title: wt（跟踪和监视数据）
description: Wt 命令通过整个函数运行，然后在函数调用开始时执行此命令时显示统计信息。
keywords:
- wt (跟踪和监视数据) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wt (Trace and Watch Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8af27f795d29cce758ec7524fe1852c91e52733d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815211"
---
# <a name="wt-trace-and-watch-data"></a>wt（跟踪和监视数据）


**Wt** 命令通过整个函数运行，然后在函数调用开始时执行此命令时显示统计信息。

```dbgcmd
wt [WatchOptions] [= StartAddress] [EndAddress] 
```

## <a name="span-idddk_cmd_trace_and_watch_data_dbgspanspan-idddk_cmd_trace_and_watch_data_dbgspanparameters"></a><span id="ddk_cmd_trace_and_watch_data_dbg"></span><span id="DDK_CMD_TRACE_AND_WATCH_DATA_DBG"></span>参数


<span id="_______WatchOptions______"></span><span id="_______watchoptions______"></span><span id="_______WATCHOPTIONS______"></span>*WatchOptions*   
指定如何修改显示。 您可以使用以下任一选项。

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
<td align="left"><p><strong>-l</strong> <em>深度</em></p></td>
<td align="left"><p>仅) 指定要显示的调用的最大深度 (用户模式。 任何深度低于开始点的 <em>深度</em> 的调用都将以无提示方式执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong> <em>模块</em></p></td>
<td align="left"><p> (用户模式仅) 将显示限制为指定模块内的代码，以及从该模块进行的第一次调用级别。 可以包含多个-m 选项以显示来自多个模块的代码，而不是其他任何模块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-i</strong> <em>模块</em></p></td>
<td align="left"><p> (用户模式仅) 忽略指定模块中的任何代码。 可以包含多个-i 选项，以忽略多个模块中的代码。 如果使用-m 选项，调试器将忽略所有-i 选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ni</strong></p></td>
<td align="left"><p> (用户模式仅) 不会将任何项显示到由于-m 或-i 选项而被忽略的代码中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-nc</strong></p></td>
<td align="left"><p>不显示单独的调用信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ns</strong></p></td>
<td align="left"><p>不显示摘要信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-nw</strong></p></td>
<td align="left"><p>跟踪期间不显示警告。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-oa</strong></p></td>
<td align="left"><p> (用户模式仅) 显示调用站点的实际地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-或</strong></p></td>
<td align="left"><p> (用户模式仅) 显示所调用函数的返回寄存器值（使用默认基数作为基）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-或</strong></p></td>
<td align="left"><p> (用户模式仅) 显示所调用函数的返回寄存器值（在每个返回值的相应类型中）。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定调试器开始执行的地址。 如果不使用 *StartAddress*，则将从指令指针指向的指令开始执行。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______EndAddress______"></span><span id="_______endaddress______"></span><span id="_______ENDADDRESS______"></span>*EndAddress*   
指定跟踪结束的地址。 如果不使用 *EndAddress*，则执行单个指令或函数调用。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p></p>
<strong>用户模式：</strong> 所有 <strong>内核模式：</strong> 仅基于 x86</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关发出 **wt** 命令和相关命令的概述的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

如果需要有关特定函数行为的信息，但不希望单步执行函数，则 **wt** 命令非常有用。 相反，请转到该函数的开头，然后发出 **wt** 命令。

如果程序计数器所在的点与符号 (如函数或入口点到模块) 的开头，则 **wt** 命令将一直跟踪直到到达当前的返回地址。 如果程序计数器在 **调用** 指令上，则 **wt** 命令将一直跟踪，直到其返回到当前位置。 [调试程序](debugger-command-window.md)中分析了此跟踪命令窗口，以及描述该命令遇到的各种调用的输出。

如果在函数开头以外的位置发出 **wt** 命令，则命令的行为类似于 [**p (步骤)**](p--step-.md) 命令。 但是，如果指定 *EndAddress*，则执行将继续直到到达该地址，即使此执行涉及许多程序步骤和函数调用。

在源模式下进行调试时，只应跟踪到函数体的左括号所在的点。 然后，可以使用 **wt** 命令。  (通常可以更轻松地在函数的第一行插入断点，或使用 "调试" [|运行至光标处](debug---run-to-cursor.md)，然后使用 **wt** 命令。 ) 

由于 **wt** 的输出可能很长，因此你可能希望使用日志文件来记录输出。

下面的示例显示了一个典型的日志文件。

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

在跟踪列表中，第一个数字指定已执行的指令数，第二个数字指定该函数的子进程执行的指令数，第三个数字 (括在括号中) 指定堆栈中的函数深度， (将初始函数作为零) 。 函数名称的缩进显示调用深度。

在前面的示例中， **MyModule！ myFunction** 将在调用多个子例程（包括 **printf** 和 **fgets**）之前执行105说明，然后在调用这些函数后执行54545个其他说明，然后发出一些更多的调用。 但是，在最后的计数中，显示屏显示 **myFunction** 执行112379指令，因为此计数包括 **myFunction** 及其子级执行的所有说明。  (**MyFunction** 的 *子级* 是直接或间接从 **myFunction** 调用的函数 ) 

在前面的示例中，另请注意， **ILT + 1440 (\_ \_ isatty)** 称为21次。 在最后一次计数中，此函数的行为的摘要显示了调用此函数的次数、任意单个执行中的最小指令数、任意单个执行的指令数最多，以及每次执行的平均指令数。

如果进行了任何系统调用，它们将出现在计数器中，并在命令输出的末尾再次列出。

 

 





