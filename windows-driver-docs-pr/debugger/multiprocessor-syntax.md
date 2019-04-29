---
title: 多处理器语法
description: 本主题介绍了包含多个处理器语法
ms.assetid: 71adc522-f078-457c-8bc9-9e971e914a41
keywords: 多处理器计算机多处理器，命令语法，双处理器计算机的命令，处理器标识符语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c76c200699c287359f4d50167f4a8d58175b2da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351791"
---
# <a name="multiprocessor-syntax"></a>多处理器语法


## <span id="ddk_multiprocessor_syntax_dbg"></span><span id="DDK_MULTIPROCESSOR_SYNTAX_DBG"></span>


KD 和内核模式 WinDbg 支持多个处理器进行调试。 您可以执行这种类型的任何多处理器平台上进行调试。

处理器编号为 0 到*n*。

如果当前处理器是处理器 0 （即，如果当前是处理器导致调试器处于活动状态），您可以检查其他非当前处理器 (处理器一个通过*n*)。 但是，您无法更改非当前处理器中的任何内容。 您只能查看其状态。

### <a name="span-idselectingaprocessorspanspan-idselectingaprocessorspanselecting-a-processor"></a><span id="selecting_a_processor"></span><span id="SELECTING_A_PROCESSOR"></span>选择一个处理器

可以使用[ **.echocpunum （显示 CPU 数）** ](-echocpunum--show-cpu-number-.md)命令以显示当前处理器的处理器数。 此命令的输出，可立即通知多处理器系统上工作的内核调试提示中的文本时。

在以下示例中， **0:** 前面**kd&gt;** 提示符指示你正在调试的计算机中的第一个处理器。

```dbgcmd
0: kd>
```

使用[ **~ s （更改当前处理器）** ](-s--change-current-processor-.md)命令处理器，如以下示例所示之间进行切换。

```dbgcmd
0: kd> ~1s
1: kd>
```

现在正在调试的计算机中的第二个处理器。

您可能必须更改多处理器系统上的处理器，如果遇到中断，并且不能理解的堆栈跟踪。 可能是另一个处理器上发生中断。

### <a name="span-idspecifyingprocessorsinothercommandsspanspan-idspecifyingprocessorsinothercommandsspanspecifying-processors-in-other-commands"></a><span id="specifying_processors_in_other_commands"></span><span id="SPECIFYING_PROCESSORS_IN_OTHER_COMMANDS"></span>在其他命令中指定的处理器

可以添加多个命令之前处理器数目。 此数字不前面是波形符 (**~**)，除非在 **~ S**命令。

**请注意**  波形符用于在用户模式下调试中，指定线程。 有关此语法的详细信息，请参阅[线程语法](thread-syntax.md)。

 

处理器 Id 无需显式引用。 相反，可以使用数值表达式解析为一个整数，对应于处理器 id。 若要指示应将表达式解释为一个处理器，请使用以下语法。

```dbgcmd
||[Expression]
```

在此语法中，方括号是必需的并且*表达式*代表的任何数值表达式，将解析为一个整数，对应于处理器 id。

在以下示例中，处理器更改具体取决于用户定义的伪寄存器的值。

```dbgcmd
||[@$t0]
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的示例使用[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令以显示从两个处理器的堆栈跟踪。

```dbgcmd
1: kd> 2k 
```

下面的示例使用[ **r （寄存器）** ](r--registers-.md)命令以显示**eax**的三个处理器的寄存器。

```dbgcmd
1: kd> 3r eax 
```

但是，以下命令提供一个语法错误，因为不能更改当前处理器之外处理器的状态。

```dbgcmd
1: kd> 3r eax=808080 
```

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>断点

内核调试，期间[**最佳实践、 bu、 bm （设置断点）** ](bp--bu--bm--set-breakpoint-.md)并[ **ba （中断的访问权限）** ](ba--break-on-access-.md)命令应用于的所有处理器多处理器计算机。

例如，如果当前处理器为三个，则可以输入以下命令以放置一个断点处**SomeAddress**。

```dbgcmd
1: kd> bp SomeAddress 
```

然后，在该地址执行的任何处理器 （不只对处理器一个） 会导致断点陷阱。

### <a name="span-iddisplayingprocessorinformationspanspan-iddisplayingprocessorinformationspandisplaying-processor-information"></a><span id="displaying_processor_information"></span><span id="DISPLAYING_PROCESSOR_INFORMATION"></span>显示处理器信息

可以使用[ **！ 运行**](-running.md)扩展以在目标计算机上显示的每个处理器的状态。 为每个处理器 **！ 运行**还可以显示从进程控制块 (PRCB) 为 16 个状态的当前和下一个线程字段内置排队自旋锁和堆栈跟踪。

可以使用[ **！ cpuinfo** ](-cpuinfo.md)并[ **！ cpuid** ](-cpuid.md)要显示有关自身的处理器信息的扩展。

 

 





