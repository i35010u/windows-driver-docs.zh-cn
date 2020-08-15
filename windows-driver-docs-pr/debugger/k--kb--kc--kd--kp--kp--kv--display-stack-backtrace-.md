---
title: k、kb、kc、kd、kp、kP、kv（显示堆栈回溯）
description: K * 命令显示给定线程的堆栈帧以及相关信息。
ms.assetid: 1061015f-cb0c-490b-b256-e0dedb659f22
keywords:
- k、kb、glm-kc-qnw、kd、kp、kP、kv (显示堆栈 Backtrace) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b63582bf6728f5dd3332009a165dcb77e1a11157
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253113"
---
# <a name="k-kb-kc-kd-kp-kp-kv-display-stack-backtrace"></a>k、kb、kc、kd、kp、kP、kv（显示堆栈回溯）


**K \* **命令显示给定线程的堆栈帧以及相关信息。

用户模式，x86 处理器

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr StackPtr InstructionPtr
[~Thread] kd [WordCount]
```

内核模式，x86 处理器

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr StackPtr InstructionPtr
[Processor] kd [WordCount]
```

用户模式、x64 处理器

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[~Thread] kd [WordCount]
```

内核模式、x64 处理器

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[Processor] kd [WordCount]
```

用户模式，ARM 处理器

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[~Thread] kd [WordCount]
```

内核模式，ARM 处理器

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[Processor] kd [WordCount]
```

## <a name="span-idddk_cmd_display_stack_backtrace_dbgspanspan-idddk_cmd_display_stack_backtrace_dbgspanparameters"></a><span id="ddk_cmd_display_stack_backtrace_dbg"></span><span id="DDK_CMD_DISPLAY_STACK_BACKTRACE_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要显示其堆栈的线程。 如果省略此参数，则显示当前线程的堆栈。 有关线程语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定要显示其堆栈的处理器。 有关处理器语法的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。

<span id="_______b"></span><span id="_______B"></span> b  
显示传递到堆栈跟踪中的每个函数的前三个参数。

<span id="_______c"></span><span id="_______C"></span> ansi-c  
显示干净堆栈跟踪。 每个显示行只包含模块名称和函数名称。

<span id="_______p"></span><span id="_______P"></span> h-p  
显示在堆栈跟踪中调用的每个函数的所有参数。 参数列表包括每个参数的数据类型、名称和值。 P 选项区分大小写。 此参数需要完整的符号信息。

<span id="_______P"></span><span id="_______p"></span> H-p  
显示堆栈跟踪中调用的每个函数的所有参数，如 p 参数。 但对于 P，将在显示的第二行上打印函数参数，而不是在与其余数据相同的行上打印。

<span id="_______v______"></span><span id="_______V______"></span> 向量   
显示框架指针省略 (FPO) 信息。 在基于 x86 的处理器上，显示还包含调用约定信息。

<span id="_______n______"></span><span id="_______N______"></span> 北   
显示帧号。

<span id="_______f______"></span><span id="_______F______"></span> 果   
显示相邻帧之间的距离。 此距离是将实际堆栈上的帧分隔的字节数。

<span id="_______L______"></span><span id="_______l______"></span> L   
隐藏显示中的源行。 L 区分大小写。

<span id="_______M"></span><span id="_______m"></span> 年  
使用 [调试器标记语言](debugger-markup-language-commands.md)显示输出。 显示中的每个帧号都是一个链接，你可以选择该链接来设置本地上下文并显示局部变量。 有关本地上下文的信息，请参阅 [**frame**](-frame--set-local-context-.md)。

<span id="_______FrameCount______"></span><span id="_______framecount______"></span><span id="_______FRAMECOUNT______"></span>*FrameCount*   
指定要显示的堆栈帧的数目。 你应以十六进制格式指定此数字，除非已使用 [**n (Set Number Base) **](n--set-number-base-.md) 命令更改了基数。 默认值为 20 (0x14) ，除非已使用 [**. kframes (Set Stack Length) **](-kframes--set-stack-length-.md) 命令更改了默认值。

<span id="_______BasePtr______"></span><span id="_______baseptr______"></span><span id="_______BASEPTR______"></span>*BasePtr*   
指定堆栈跟踪的基指针。 仅当命令后面有一个等号 (=) 时， *BasePtr* 参数才可用。

<span id="_______StackPtr______"></span><span id="_______stackptr______"></span><span id="_______STACKPTR______"></span>*StackPtr*   
指定堆栈跟踪的堆栈指针。 如果省略 *StackPtr* 和 *InstructionPtr*，则该命令将使用 rsp (或 esp) register 指定的堆栈指针，以及 rip (或 eip) register 指定的指令指针。

<span id="_______InstructionPtr______"></span><span id="_______instructionptr______"></span><span id="_______INSTRUCTIONPTR______"></span>*InstructionPtr*   
指定堆栈跟踪的指令指针。 如果省略 *StackPtr* 和 *InstructionPtr*，则该命令将使用 rsp (或 esp) register 指定的堆栈指针，以及 rip (或 eip) register 指定的指令指针。

<span id="_______WordCount______"></span><span id="_______wordcount______"></span><span id="_______WORDCOUNT______"></span>*WordCount*   
指定 \_ 堆栈中要转储的 DWORD PTR 值的数量。 默认值为 20 (0x14) ，除非你使用 [**. kframes (Set Stack Length) **](-kframes--set-stack-length-.md) 命令更改了默认值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_information1spanspan-idadditional_information1spanadditional-information"></a><span id="additional_information1"></span><span id="ADDITIONAL_INFORMATION1"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

发出 **k**、 **kb**、 **kp**、 **kp**或 **kv** 命令时，会以表格格式显示堆栈跟踪。 如果启用行加载，还会显示源模块和行号。

堆栈跟踪包括堆栈帧的基指针、返回地址和函数名称。

如果使用 **kp** 或 **kp** 命令，则将显示在堆栈跟踪中调用的每个函数的完整参数。 参数列表包括每个参数的数据类型、名称和值。

此命令可能会很慢。 例如，当 **MyFunction1** 调用 **MyFunction2**时，调试程序必须具有 **MyFunction1** 的完整符号信息以显示在此调用中传递的参数。 此命令不会完全显示公共符号中未公开的内部 Microsoft Windows 例程。

如果使用 **kb** 或 **kv** 命令，则会显示传递给每个函数的前三个参数。 如果使用 **kv** 命令，则还会显示 FPO 数据。

在基于 x86 的处理器上， **kv** 命令还显示调用约定信息。

当你使用 **kv** 命令时，将在行的末尾添加 FPO 信息，格式如下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">FPO 文本</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">FPO： [非 Fpo]</td>
<td align="left"><p>该帧没有 FPO 数据。</p></td>
</tr>
<tr class="even">
<td align="left">FPO： [N1，N2，N3]</td>
<td align="left"><p><em>N1</em> 是参数的总数。</p>
<p><em>N2</em> 是局部变量的 DWORD 值数。</p>
<p><em>N3</em> 是已保存的寄存器的数目。</p></td>
</tr>
<tr class="odd">
<td align="left">FPO： [N1，N2] TrapFrame @ Address</td>
<td align="left"><p><em>N1</em> 是参数的总数。</p>
<p><em>N2</em> 是局部变量的 DWORD 值的数目。</p>
<p><em>Address</em> 是捕获帧的地址。</p></td>
</tr>
<tr class="even">
<td align="left">FPO： TaskGate 段：0</td>
<td align="left"><p><em>段</em> 是任务入口的段选择器。</p></td>
</tr>
<tr class="odd">
<td align="left">FPO： [EBP 0xBase]</td>
<td align="left"><p><em>Base</em> 是框架的基指针。</p></td>
</tr>
</tbody>
</table>

 

**Kd**命令显示原始堆栈数据。 每个 DWORD 值都显示在单独的行上。 将为这些行以及关联符号显示符号信息。 此格式将创建比其他**k**命令更详细的列表 _\*_ 。 **Kd**命令等效于[**Dds (显示内存) **](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令，该命令使用堆栈地址作为其参数。

如果在函数 prolog 的开头使用 **k** 命令 (在) 上执行函数 prolog 之前，会收到不正确的结果。 调试器使用帧寄存器来计算当前 backtrace，并且在执行函数的 prolog 之前，此寄存器的设置不正确。

在用户模式下，堆栈跟踪基于当前线程的堆栈。 有关线程的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，堆栈跟踪基于当前的 [注册表上下文](changing-contexts.md#register-context)。 您可以将注册上下文设置为与特定线程、上下文记录或捕获帧匹配。

### <a name="span-idadditional_information2spanspan-idadditional_information2spanadditional-information"></a><span id="additional_information2"></span><span id="ADDITIONAL_INFORMATION2"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

 

 





