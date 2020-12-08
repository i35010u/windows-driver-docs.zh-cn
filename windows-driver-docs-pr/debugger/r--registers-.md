---
title: r（寄存器）
description: R 命令显示或修改寄存器、浮点寄存器、标志、伪寄存器和固定名称的别名。
keywords:
- r (注册) Windows 调试
ms.date: 07/11/2018
topic_type:
- apiref
api_name:
- r (Registers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07f33cd6cff8432ee483e2f81c493c8b8f639dd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839797"
---
# <a name="r-registers"></a>r（寄存器）


**R** 命令显示或修改寄存器、浮点寄存器、标志、伪寄存器和固定名称的别名。

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

## <a name="span-idddk_cmd_registers_dbgspanspan-idddk_cmd_registers_dbgspanparameters"></a><span id="ddk_cmd_registers_dbg"></span><span id="DDK_CMD_REGISTERS_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定从中读取寄存器的处理器。 默认值为零。 如果指定 *Processor*，则不能包含 *注册* 参数-将显示所有寄存器。 有关语法的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。 只能在内核模式下指定处理器。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定从中读取寄存器的线程。 如果未指定线程，则使用当前线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______M_______Mask______"></span><span id="_______m_______mask______"></span><span id="_______M_______MASK______"></span>**M** *Mask*   
指定调试器显示寄存器时要使用的掩码。 "M" 必须为大写字母。 *掩码* 是指示寄存器显示内容的位的总和。 位的含义取决于处理器和模式 (查看以下 "备注" 部分中的表，以了解详细信息) 。 如果省略 **M**，则使用默认掩码。 您可以使用 [**Rm (注册掩码)**](rm--register-mask-.md) 命令设置或显示默认掩码。

<span id="_______F______"></span><span id="_______f______"></span>**F**   
显示浮点寄存器。 "F" 必须为大写字母。 此选项与 **M 0x4** 等效。

<span id="_______X______"></span><span id="_______x______"></span>**X**   
显示 SSE XMM 寄存器。 此选项与 **M 0x40** 等效。

<span id="_______Y______"></span><span id="_______y______"></span>**Y**   
显示 AVX YMM 寄存器。 此选项与 **M 0x200** 等效。

<span id="_______YI______"></span><span id="_______yi______"></span>**彝语**   
显示 AVX YMM 整数寄存器。 此选项与 **M 0x400** 等效。

<span id="_______YI______"></span><span id="_______yi______"></span>**Z**   
以浮点格式显示 AVX-512 YMM 寄存器 (zmm0-zmm31) 。 

<span id="_______YI______"></span><span id="_______yi______"></span>**ZI**   
显示整数格式 (zmm0-zmm31) 的 512 AVX YMM 寄存器。 

<span id="_______YI______"></span><span id="_______yi______"></span>**K**   
显示 AVX-512 Opmask 谓词注册 (K0-K7) 。

<span id="______________"></span> **?**   
仅 (伪寄存器分配) 会导致伪寄存器获取类型化信息。 允许任何类型。 有关 **r？** 语法的详细信息，请参阅 [调试器命令程序示例](debugger-command-program-examples.md)。

<span id="_______Register______"></span><span id="_______register______"></span><span id="_______REGISTER______"></span>*注册*   
指定要显示或修改的注册、标志、伪寄存器或固定名称别名。 不能在此参数前面加上 (**@**) 符号。 有关语法的详细信息，请参阅 [Register 语法](register-syntax.md)。

<span id="_______Num______"></span><span id="_______num______"></span><span id="_______NUM______"></span>*Num*   
指定要显示的元素的数目。 如果省略此参数，但包含 *类型*，则会显示完整寄存器长度。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定要在其中显示每个 register 元素的数据格式。 只能将 *Type* 用于64位和128位矢量寄存器。 可以指定多个类型。

可以指定以下一个或多个值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>类型</em></th>
<th align="left">显示格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ib</strong></p></td>
<td align="left"><p>带符号字节</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ub</strong></p></td>
<td align="left"><p>无符号字节</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iw</strong></p></td>
<td align="left"><p>带符号字词</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uw</strong></p></td>
<td align="left"><p>无符号字词</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>id</strong></p></td>
<td align="left"><p>带符号 DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ud</strong></p></td>
<td align="left"><p>无符号 DWORD</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iq</strong></p></td>
<td align="left"><p>带符号四字</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uq</strong></p></td>
<td align="left"><p>无符号四字</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>f</strong></p></td>
<td align="left"><p>32位浮点</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>64位浮点</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定要分配给寄存器的值。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

 **.**   
显示当前指令中使用的寄存器。 如果未使用任何寄存器，则不会显示任何输出。

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
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

如果未指定 *Register*，则 **r** 命令将显示所有非浮点寄存器，并且 **rF** 命令显示所有浮点寄存器。 您可以使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令来更改此行为。

如果指定 *register* 但省略等号 (=) 和 *Value* 参数，则该命令将显示寄存器的当前值。

如果指定 *register* ，并使用等号 (=) 但省略了 *value*，则该命令将显示注册的当前值并提示输入新值。

如果指定 *register*、等号 (=) 和 *值*，则该命令会更改寄存器以包含值。  (如果 *静默模式* 处于活动状态，则可以省略等号。 您可以使用 [**sq (设置静默模式)**](sq--set-quiet-mode-.md) 命令打开静默模式。 在内核模式下，还可以通过使用 KDQUIET [环境变量](kernel-mode-environment-variables.md)来打开静默模式。 ) 

可以指定多个寄存器，用逗号分隔。

在用户模式下， **r** 命令显示与当前线程关联的寄存器。 有关线程的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下， **r** 命令显示与当前 *注册上下文* 关联的寄存器。 您可以将注册上下文设置为与特定线程、上下文记录或捕获帧匹配。 对于指定的寄存器上下文，只显示最重要的寄存器，并且您无法更改其值。 有关注册上下文的详细信息，请参阅 [注册上下文](changing-contexts.md#register-context)。

按名称指定浮点寄存器时，不需要 **F** 选项。 指定单个浮点寄存器时，除了显示十进制值外，还会显示原始的十六进制值。

基于 x86 的处理器或基于 x64 的处理器支持以下 *掩码* 位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit</th>
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
0 1</td>
<td align="left"><p></p>
0x1 0x2</td>
<td align="left"><p>显示基本整数寄存器。  (设置其中一个或两个位具有相同的效果。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x4</p></td>
<td align="left"><p>显示浮点寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>显示段寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>显示 MMX 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>显示调试寄存器。 在内核模式下，设置此位也会显示 CR4 注册。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>显示 SSE XMM 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>仅) 显示控制寄存器 (内核模式，例如 CR0、CR2、CR3 和 CR8。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x100</p></td>
<td align="left"><p> (内核模式仅) 显示描述符和任务状态寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"><p>显示浮点数中的 AVX YMM 寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>0x400</p></td>
<td align="left"><p>以十进制整数显示 AVX YMM 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>11</p></td>
<td align="left"><p>0x800</p></td>
<td align="left"><p>以十进制整数显示 AVX XMM 寄存器。</p></td>
</tr>
</tbody>
</table>


 

下面的代码示例演示了基于 x86 的处理器的 **r** 命令。

在内核模式下，以下命令显示处理器2的寄存器。

```dbgcmd
1: kd> 2r 
```

在用户模式下，以下命令显示线程2的寄存器。

```dbgcmd
0:000> ~2 r 
```

在用户模式下，下面的命令显示与线程索引顺序) 中的所有线程关联的所有 **eax** 寄存器 (。

```dbgcmd
0:000> ~* r eax
```

以下命令将当前线程的 **eax** 寄存器设置为0x000000FF。

```dbgcmd
0:000> r eax=0x000000FF
```

以下命令将 **st0** 寄存器设置为 1.234 e + 10 (**F** 是可选) 。

```dbgcmd
0:000> rF st0=1.234e+10
```

以下命令显示零标志。

```dbgcmd
0:000> r zf 
```

以下命令将 **xmm0** register 显示为16个无符号字节，然后以双精度浮点格式显示 **xmm1** 寄存器的全部内容。

```dbgcmd
0:000> r xmm0:16ub, xmm1:d 
```

如果当前语法为 c + +，则必须在寄存器之前 **@**)  (。 因此，您可以使用以下命令将 **ebx** 注册复制到 **eax** 寄存器。

```dbgcmd
0:000> r eax = @ebx
```

以下命令显示了伪寄存器，其方式与 **r** 命令显示寄存器的方式相同。

```dbgcmd
0:000> r $teb
```

你还可以使用 **r** 命令创建 *固定名称别名*。 这些别名不是寄存器或伪寄存器，即使它们与 **r** 命令相关联。 有关这些别名的详细信息，请参阅 [使用别名](using-aliases.md)。

下面是 r 的示例 **。** 基于 x86 的处理器上的命令。 调用堆栈的最后一项在命令本身之前。

```dbgcmd
01004af3 8bec            mov     ebp,esp
0:000> r.
ebp=0006ffc0  esp=0006ff7c
```


 

 





