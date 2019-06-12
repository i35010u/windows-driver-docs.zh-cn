---
title: k、kb、kc、kd、kp、kP、kv（显示堆栈回溯）
description: K * 命令将显示给定线程，以及相关信息的堆栈帧。
ms.assetid: 1061015f-cb0c-490b-b256-e0dedb659f22
keywords:
- k、 kb、 kc、 kd、 kp，kP、 kv （显示堆栈回溯） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fad326f48550d25c1e91a806e787b9da703e811d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367231"
---
# <a name="k-kb-kc-kd-kp-kp-kv-display-stack-backtrace"></a>k、kb、kc、kd、kp、kP、kv（显示堆栈回溯）


<strong>K *\\</strong>* * 命令将显示给定线程，以及相关信息的堆栈帧...

用户模式下，x86 处理器

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr StackPtr InstructionPtr
[~Thread] kd [WordCount]
```

内核模式下，x86 处理器

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr StackPtr InstructionPtr
[Processor] kd [WordCount]
```

用户模式下，x64 处理器

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[~Thread] kd [WordCount]
```

内核模式下，x64 处理器

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[Processor] kd [WordCount]
```

用户模式下，ARM 处理器

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

## <a name="span-idddkcmddisplaystackbacktracedbgspanspan-idddkcmddisplaystackbacktracedbgspanparameters"></a><span id="ddk_cmd_display_stack_backtrace_dbg"></span><span id="DDK_CMD_DISPLAY_STACK_BACKTRACE_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定要显示其堆栈的线程。 如果省略此参数，则显示当前线程的堆栈。 有关线程语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定其堆栈未显示的处理器。 有关处理器语法的详细信息，请参阅[包含多个处理器语法](multiprocessor-syntax.md)。

<span id="_______b"></span><span id="_______B"></span> b  
显示传递到堆栈跟踪中的每个函数的前三个参数。

<span id="_______c"></span><span id="_______C"></span> c  
显示清理堆栈跟踪。 每个显示行包括仅模块名称和函数名称。

<span id="_______p"></span><span id="_______P"></span> p  
显示每个函数的参数的所有堆栈跟踪中。 参数列表包括每个参数的数据类型、 名称和值。 P 选项是区分大小写。 此参数要求的完整符号信息。

<span id="_______P"></span><span id="_______p"></span> P  
显示每个函数的参数的所有堆栈跟踪，如 p 参数中。 但是，为 P，函数参数都显示在第二行显示，而不是数据的其余部分所在的同一行上。

<span id="_______v______"></span><span id="_______V______"></span> v   
显示帧指针省略 (FPO) 信息。 在基于 x86 的处理器中，显示内容还包括调用约定的信息。

<span id="_______n______"></span><span id="_______N______"></span> n   
显示帧号。

<span id="_______f______"></span><span id="_______F______"></span> f   
显示相邻的帧之间的距离。 此距离是单独的端口上的实际堆栈帧的字节数。

<span id="_______L______"></span><span id="_______l______"></span> L   
隐藏在显示中的源行。 L 是区分大小写。

<span id="_______M"></span><span id="_______m"></span> M  
显示使用的输出[调试器标记语言](debugger-markup-language-commands.md)。 在显示中的每个帧数是可以单击来设置本地上下文和显示本地变量的链接。 有关本地上下文的信息，请参阅[ **.frame**](-frame--set-local-context-.md)。

<span id="_______FrameCount______"></span><span id="_______framecount______"></span><span id="_______FRAMECOUNT______"></span> *FrameCount*   
指定要显示的堆栈帧数。 应以十六进制格式指定此数字，除非已使用更改基数[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。 默认值为 20 (0x14)，除非已使用更改默认值[ **.kframes （设置堆栈长度）** ](-kframes--set-stack-length-.md)命令。

<span id="_______BasePtr______"></span><span id="_______baseptr______"></span><span id="_______BASEPTR______"></span> *BasePtr*   
指定堆栈跟踪的基的指针。 *BasePtr*参数是该命令之后没有等号 （=） 时才可用。

<span id="_______StackPtr______"></span><span id="_______stackptr______"></span><span id="_______STACKPTR______"></span> *StackPtr*   
指定的堆栈跟踪的堆栈指针。 如果省略*StackPtr*并*InstructionPtr*，该命令使用 rsp （或 esp） 注册指定的堆栈指针和翻录 （或 eip） 注册指定的指令指针。

<span id="_______InstructionPtr______"></span><span id="_______instructionptr______"></span><span id="_______INSTRUCTIONPTR______"></span> *InstructionPtr*   
指定指令指针的堆栈跟踪。 如果省略*StackPtr*并*InstructionPtr*，该命令使用 rsp （或 esp） 注册指定的堆栈指针和翻录 （或 eip） 注册指定的指令指针。

<span id="_______WordCount______"></span><span id="_______wordcount______"></span><span id="_______WORDCOUNT______"></span> *WordCount*   
指定的双字节数\_PTR 堆栈转储中的值。 默认值为 20 (0x14)，除非通过使用更改默认值，否则[ **.kframes （设置堆栈长度）** ](-kframes--set-stack-length-.md)命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformation1spanspan-idadditionalinformation1spanadditional-information"></a><span id="additional_information1"></span><span id="ADDITIONAL_INFORMATION1"></span>其他信息

有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

当您发出**k**， **kb**， **kp**， **kP**，或**kv**命令时，堆栈跟踪显示在表格格式。 如果启用了行加载，也会显示源代码模块和行号。

堆栈跟踪包含堆栈帧、 回邮地址和函数名称的基指针。

如果您使用**kp**或**kP**命令时，显示调用堆栈跟踪中的每个函数的完整参数。 参数列表包括每个参数的数据类型、 名称和值。

此命令可能很慢。 例如，当**MyFunction1**调用**MyFunction2**，调试器必须具有完整符号信息**MyFunction1**若要在此显示传递参数调用。 此命令不完全显示在公共符号不公开的内部 Microsoft Windows 例程。

如果您使用**kb**或**kv**命令时，显示传递给每个函数的前三个参数。 如果您使用**kv**命令时，还显示 FPO 数据。

在基于 x86 的处理器上， **kv**命令还显示调用约定信息。

当你使用**kv**命令，在采用以下格式的行的末尾添加 FPO 信息。

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
<td align="left">FPO: [非 Fpo]</td>
<td align="left"><p>没有 FPO 的数据帧。</p></td>
</tr>
<tr class="even">
<td align="left">FPO: [N1，N2，N3]</td>
<td align="left"><p><em>N1</em>是参数的总数。</p>
<p><em>N2</em>是本地变量的 DWORD 值的数目。</p>
<p><em>N3</em>是保存的寄存器的数目。</p></td>
</tr>
<tr class="odd">
<td align="left">FPO: [N1，N2] TrapFrame @ 地址</td>
<td align="left"><p><em>N1</em>是参数的总数。</p>
<p><em>N2</em>局部变量是 DWORD 值的数目。</p>
<p><em>地址</em>是陷阱帧的地址。</p></td>
</tr>
<tr class="even">
<td align="left">FPO:TaskGate 段： 0</td>
<td align="left"><p><em>段</em>是为任务入口段选择器。</p></td>
</tr>
<tr class="odd">
<td align="left">FPO: [EBP 0xBase]</td>
<td align="left"><p><em>基</em>是帧的基指针。</p></td>
</tr>
</tbody>
</table>

 

**Kd**命令显示原始堆栈的数据。 单独的行上显示每个 DWORD 值。 为这些行与相关联的符号一起显示符号信息。 此格式创建比另一个更详细的列表 **k * * *\** 命令。 **Kd**命令等效于[ **dds （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)使用堆栈地址作为其参数的命令。

如果您使用**k**命令函数 （之前已执行函数 prolog） 的开始处收到不正确的结果。 调试器使用帧寄存器来计算当前反向跟踪，并且此寄存器才会设置正确的函数执行其 prolog。

在用户模式下，堆栈跟踪基于当前线程的堆栈。 有关线程的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，堆栈跟踪基于当前[注册上下文](changing-contexts.md#register-context)。 可以设置寄存器上下文以匹配特定线程、 上下文记录或捕获帧。

### <a name="span-idadditionalinformation2spanspan-idadditionalinformation2spanadditional-information"></a><span id="additional_information2"></span><span id="ADDITIONAL_INFORMATION2"></span>其他信息

有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

 

 





