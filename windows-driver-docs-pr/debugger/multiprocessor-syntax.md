---
title: 多处理器语法
description: 本主题介绍多处理器语法
ms.assetid: 71adc522-f078-457c-8bc9-9e971e914a41
keywords: 多处理器计算机，多处理器，命令语法，双处理器计算机，命令语法规则，处理器标识符
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c76c200699c287359f4d50167f4a8d58175b2da
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242790"
---
# <a name="multiprocessor-syntax"></a>多处理器语法


## <span id="ddk_multiprocessor_syntax_dbg"></span><span id="DDK_MULTIPROCESSOR_SYNTAX_DBG"></span>


KD 和内核模式 WinDbg 支持多处理器调试。 可以在任何多处理器平台上执行此类调试。

处理器的编号为0到*n*。

如果当前处理器为处理器0（即，如果它是当前导致调试器处于活动状态的处理器），则可以检查其他非当前处理器（从1到*n*）。 但是，不能更改非当前处理器中的任何内容。 只能查看其状态。

### <a name="span-idselecting_a_processorspanspan-idselecting_a_processorspanselecting-a-processor"></a><span id="selecting_a_processor"></span><span id="SELECTING_A_PROCESSOR"></span>选择处理器

可以使用[**echocpunum （显示 CPU 号）** ](-echocpunum--show-cpu-number-.md)命令显示当前处理器的处理器号。 使用此命令的输出，你可以立即了解内核调试提示中的文本处理多处理器系统的时间。

在下面的示例中， **0：** 在**kd&gt;** 提示前面，指示正在调试计算机中的第一个处理器。

```dbgcmd
0: kd>
```

使用[ **~ s （更改当前处理器）** ](-s--change-current-processor-.md)命令在处理器之间切换，如下面的示例所示。

```dbgcmd
0: kd> ~1s
1: kd>
```

现在正在调试计算机中的第二个处理器。

如果遇到中断并且无法理解堆栈跟踪，则可能必须更改多处理器系统上的处理器。 中断可能发生在不同的处理器上。

### <a name="span-idspecifying_processors_in_other_commandsspanspan-idspecifying_processors_in_other_commandsspanspecifying-processors-in-other-commands"></a><span id="specifying_processors_in_other_commands"></span><span id="SPECIFYING_PROCESSORS_IN_OTHER_COMMANDS"></span>在其他命令中指定处理器

你可以在多个命令前添加一个处理器编号。 此数字前面不带有波形符（ **~** ），只在 **~ S**命令中例外。

**注意**   在用户模式调试中，使用波形符来指定线程。 有关此语法的详细信息，请参阅[线程语法](thread-syntax.md)。

 

处理器 Id 无需显式引用。 相反，可以使用解析为与处理器 ID 对应的整数的数值表达式。 若要指示表达式应解释为处理器，请使用以下语法。

```dbgcmd
||[Expression]
```

在此语法中，方括号是必需的，并且*Expression*表示解析为对应于处理器 ID 的整数的任何数值表达式。

在下面的示例中，处理器将根据用户定义的伪寄存器的值发生变化。

```dbgcmd
||[@$t0]
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的示例使用[**k （显示 Stack Backtrace）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令显示 processor 2 中的堆栈跟踪。

```dbgcmd
1: kd> 2k 
```

下面的示例使用[**r （寄存器）** ](r--registers-.md)命令显示 processor 3 的**eax**寄存器。

```dbgcmd
1: kd> 3r eax 
```

但是，下面的命令会导致语法错误，因为无法更改当前处理器以外的其他处理器的状态。

```dbgcmd
1: kd> 3r eax=808080 
```

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>处

在内核调试期间，[**最佳实践、bu、bm.exe （设置断点）** ](bp--bu--bm--set-breakpoint-.md)和[**ba （访问时中断）** ](ba--break-on-access-.md)命令适用于多处理器计算机的所有处理器。

例如，如果当前处理器为三个，则可以输入以下命令，在**SomeAddress**处放置一个断点。

```dbgcmd
1: kd> bp SomeAddress 
```

然后，在该地址执行的任何处理器（而非处理器）都将导致断点陷阱。

### <a name="span-iddisplaying_processor_informationspanspan-iddisplaying_processor_informationspandisplaying-processor-information"></a><span id="displaying_processor_information"></span><span id="DISPLAYING_PROCESSOR_INFORMATION"></span>显示处理器信息

您可以使用[ **！运行**](-running.md)扩展显示目标计算机上每个处理器的状态。 对于每个处理器， **！运行**还可以显示进程控制块（PRCB）中的当前和下一个线程字段、16个内置排队旋转锁的状态和堆栈跟踪。

您可以使用[ **！ cpuinfo**](-cpuinfo.md)和[ **！ cpuid**](-cpuid.md)扩展显示有关处理器本身的信息。

 

 





