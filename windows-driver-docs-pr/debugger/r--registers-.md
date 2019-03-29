---
title: r（寄存器）
description: R 命令显示或修改寄存器、 浮点寄存器、 标志、 伪寄存器和固定名称的别名。
ms.assetid: c0d0af2f-1852-47a4-8f01-95f6ec198112
keywords:
- r （寄存器） Windows 调试
ms.date: 07/11/2018
topic_type:
- apiref
api_name:
- r (Registers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c66fd4bb9650e9e26eb6e4a5d0aeff86da6c949
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568568"
---
# <a name="r-registers"></a>r（寄存器）


**R**命令显示或修改寄存器、 浮点寄存器、 标志、 伪寄存器和固定名称的别名。

User-Mode

```dbgcmd
[~Thread] r[M Mask|F|X|?] [ Register[:[Num]Type] [= [Value]] ] 
r.
```

Kernel-Mode

```dbgcmd
[Processor] r[M Mask|F|X|Y|YI|?] [ Register[:[Num]Type] [= [Value]] ] 
r.
```

## <a name="span-idddkcmdregistersdbgspanspan-idddkcmdregistersdbgspanparameters"></a><span id="ddk_cmd_registers_dbg"></span><span id="DDK_CMD_REGISTERS_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定从读取寄存器的处理器。 默认值为零。 如果指定*处理器*，不能包含*注册*参数-显示所有寄存器。 有关语法的详细信息，请参阅[包含多个处理器语法](multiprocessor-syntax.md)。 仅在内核模式下，可以指定处理器。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定从读取寄存器的线程。 如果不指定线程，则使用当前线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______M_______Mask______"></span><span id="_______m_______mask______"></span><span id="_______M_______MASK______"></span> **M** *掩码*   
指定要使用时，调试器显示寄存器的掩码。 "M"必须是一个大写字母。 *掩码*是位，指示有关注册显示的内容的总和。 位的含义取决于处理器和模式 （请参阅有关详细信息下的备注部分中的表）。 如果省略**M**，使用默认的掩码。 你可以设置或通过使用显示默认的掩码[ **Rm （注册掩码）** ](rm--register-mask-.md)命令。

<span id="_______F______"></span><span id="_______f______"></span> **F**   
显示浮点寄存器。 "F"必须是一个大写字母。 此选项等效于**M 0x4**。

<span id="_______X______"></span><span id="_______x______"></span> **X**   
显示 SSE XMM 寄存器。 此选项等效于**M 0x40**。

<span id="_______Y______"></span><span id="_______y______"></span> **Y**   
显示 AVX YMM 寄存器。 此选项等效于**M 0x200**。

<span id="_______YI______"></span><span id="_______yi______"></span> **YI**   
显示整数寄存器 AVX YMM。 此选项等效于**M 0x400**。

<span id="_______YI______"></span><span id="_______yi______"></span> **Z**   
浮动点格式显示 AVX-512 YMM 寄存器 (zmm0 zmm31)。 

<span id="_______YI______"></span><span id="_______yi______"></span> **ZI**   
整数格式显示 AVX-512 YMM 寄存器 (zmm0 zmm31)。 

<span id="_______YI______"></span><span id="_______yi______"></span> **K**   
显示 AVX-512 Opmask 谓词寄存器 (K0 K7)。

<span id="______________"></span> **?**   
（仅适用于伪寄存器分配）会导致伪寄存器，若要获取类型化的信息。 允许任何类型。 有关详细信息**r？** 语法，请参阅[调试器命令程序示例](debugger-command-program-examples.md)。

<span id="_______Register______"></span><span id="_______register______"></span><span id="_______REGISTER______"></span> *注册*   
指定注册、 标志、 伪寄存器或要显示或修改的固定名称别名。 必须排在与此参数 (**@**) 登录。 有关语法的详细信息，请参阅[注册语法](register-syntax.md)。

<span id="_______Num______"></span><span id="_______num______"></span><span id="_______NUM______"></span> *Num*   
指定要显示的元素数。 如果省略此参数，但您包括*类型*，显示完整的寄存器长度。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定要显示的每个注册元素的数据格式。 可以使用*类型*仅与 64 位和 128 位的矢量寄存器。 可以指定多个类型。

您可以指定一个或多个以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Type</em></th>
<th align="left">显示格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ib</strong></p></td>
<td align="left"><p>有符号的字节</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ub</strong></p></td>
<td align="left"><p>无符号的字节</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iw</strong></p></td>
<td align="left"><p>有符号的 word</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uw</strong></p></td>
<td align="left"><p>无符号的字</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>id</strong></p></td>
<td align="left"><p>有符号的 DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ud</strong></p></td>
<td align="left"><p>无符号的 DWORD</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iq</strong></p></td>
<td align="left"><p>有符号的四字</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uq</strong></p></td>
<td align="left"><p>无符号的四字</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>f</strong></p></td>
<td align="left"><p>32 位浮点</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>64 位浮点</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *值*   
指定要分配到寄存器的值。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

 **.**   
显示在当前指令中使用的寄存器。 如果不使用任何寄存器，将不显示任何输出。

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
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

如果未指定*注册*，则**r**命令显示所有非浮动点寄存器，并且**rF**命令显示所有浮点寄存器。 可以通过更改此行为[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

如果指定*注册*但省略等号 （=） 和*值*参数，则该命令显示的寄存器的当前值。

如果指定*注册*，并以等号 （=），但省略*值*，该命令显示的寄存器的当前值并会提示输入新值。

如果指定*注册*，等号 （=） 和*值*，命令将更改的寄存器来包含值。 (如果*安静模式下*是处于活动状态，则可以省略等号。 您可以使用启用安静模式下[ **sq （设置安静模式下）** ](sq--set-quiet-mode-.md)命令。 在内核模式下，您还可以在静默模式下使用 KDQUIET[环境变量](kernel-mode-environment-variables.md)。)

您可以指定多个寄存器中，用逗号隔开。

在用户模式下**r**命令将显示与当前线程相关联的寄存器。 有关线程的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下**r**命令将显示与当前相关联的寄存器*注册上下文*。 可以设置寄存器上下文以匹配特定线程、 上下文记录或捕获帧。 只有实际显示指定的寄存器上下文的最重要寄存器，并且不能更改它们的值。 有关寄存器上下文的详细信息，请参阅[注册上下文](changing-contexts.md#register-context)。

当按名称、 指定的浮点寄存器**F**选项并非必需。 当指定了单一的浮点寄存器时，除了的十进制值显示原始的十六进制值。

以下*掩码*支持基于 x86 的处理器或基于 x64 的处理器的位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
0 1</td>
<td align="left"><p></p>
0x1 0x2</td>
<td align="left"><p>显示基本整数寄存器。 （一个或两个这些位将设置有相同的效果。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x4</p></td>
<td align="left"><p>显示浮点寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>显示段寄存器信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>显示 MMX 寄存器信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>显示调试寄存器信息。 在内核模式下设置此位还显示 CR4 注册。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>显示 SSE XMM 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>（仅适用于内核模式）显示控制寄存器，例如 CR0、 CR2、 CR3 和 CR8。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x100</p></td>
<td align="left"><p>（仅适用于内核模式）显示描述符和任务状态寄存器信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"><p>AVX YMM 寄存器中浮动点的显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>0x400</p></td>
<td align="left"><p>显示 AVX YMM 寄存器中十进制整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>11</p></td>
<td align="left"><p>0x800</p></td>
<td align="left"><p>显示 AVX XMM 注册十进制整数。</p></td>
</tr>
</tbody>
</table>


 

下面的代码示例所示**r**的基于 x86 的处理器的命令。

在内核模式下，以下命令显示了 2 处理器的寄存器。

```dbgcmd
1: kd> 2r 
```

在用户模式下，以下命令显示了线程 2 的寄存器。

```dbgcmd
0:000> ~2 r 
```

在用户模式下，以下命令显示的所有**eax**寄存器所带来的所有线程 （在线程索引顺序）。

```dbgcmd
0:000> ~* r eax
```

下面的命令集**eax**注册到 0x000000FF 当前线程。

```dbgcmd
0:000> r eax=0x000000FF
```

下面的命令集**st0**注册到 1.234e + 10 ( **F**是可选的)。

```dbgcmd
0:000> rF st0=1.234e+10
```

下面的命令显示的零个标志。

```dbgcmd
0:000> r zf 
```

下面的命令显示**xmm0**注册为无符号的 16 个字节，然后显示的全部内容**xmm1**注册以双精度浮点格式。

```dbgcmd
0:000> r xmm0:16ub, xmm1:d 
```

如果当前的语法是 c + +，则必须在前面的寄存器 at 符号 (**@**)。 因此，您可以使用以下命令复制**ebx**中注册**eax**注册。

```dbgcmd
0:000> r eax = @ebx
```

下面的命令显示伪寄存器中相同的方式**r**命令可以显示寄存器。

```dbgcmd
0:000> r $teb
```

此外可以使用**r**命令，以创建*修复名称别名*。 这些别名不是寄存器或伪寄存器中，即使其关联**r**命令。 有关这些别名的详细信息，请参阅[Using 别名](using-aliases.md)。

下面是示例的**r。** 在基于 x86 的处理器上的命令。 调用堆栈的最后一项之前命令本身。

```dbgcmd
01004af3 8bec            mov     ebp,esp
0:000> r.
ebp=0006ffc0  esp=0006ff7c
```


 

 





