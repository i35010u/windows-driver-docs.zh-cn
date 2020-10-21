---
title: x86 体系结构
description: x86 体系结构
ms.assetid: 42c62647-7c9a-496e-839f-91283db73a29
keywords:
- x86 处理器，体系结构
- 在 x86 处理器上注册
- x86 处理器，寄存器
- x86 处理器，调用约定
- x86 处理器，数据类型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7da158a055960451e60d2275f2b26333db1fadc5
ms.sourcegitcommit: 89b8a43480246dd726e3632aab2db9cf2eb7505d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92254052"
---
# <a name="x86-architecture"></a>x86 体系结构


## <span id="ddk_x86_architecture_dbg"></span><span id="DDK_X86_ARCHITECTURE_DBG"></span>


Intel x86 处理器使用 (CISC) 体系结构的复杂指令集计算机，这意味着有适度数量的特殊用途寄存器，而不是大量通用寄存器。 这也意味着复杂的特殊用途说明将主流。

X86 处理器至少以8位 Intel 8080 处理器的速度跟踪其遗产。 X86 指令集中的许多 peculiarities 是由于与该处理器的向后兼容性 (及其 Zilog Z-80 变体) 。

Microsoft Win32 在 *32 位平面模式下*使用 x86 处理器。 本文档将仅重点介绍平面模式。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>寄存器

X86 体系结构由以下非特权整数寄存器组成。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>eax</strong></p></td>
<td align="left"><p>累加器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ebx</strong></p></td>
<td align="left"><p>基寄存器</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ecx</strong></p></td>
<td align="left"><p>计数器注册</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>edx</strong></p></td>
<td align="left"><p>数据注册-可用于 i/o 端口访问和算术函数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>esi</strong></p></td>
<td align="left"><p>源索引寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>edi</strong></p></td>
<td align="left"><p>目标索引寄存器</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ebp</strong></p></td>
<td align="left"><p>基指针寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>能力</strong></p></td>
<td align="left"><p>堆栈指针</p></td>
</tr>
</tbody>
</table>

 

所有整数寄存器均为32位。 但是，其中许多是16位或8位 subregisters。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ax</strong></p></td>
<td align="left"><p>低16位 <strong>eax</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bx</strong></p></td>
<td align="left"><p>低16位 <strong>ebx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cx</strong></p></td>
<td align="left"><p>最小16位 <strong>ecx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dx</strong></p></td>
<td align="left"><p>低16位 <strong>edx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p><strong>Esi</strong>的低16位</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>di</strong></p></td>
<td align="left"><p>低16位 <strong>edi</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bp</strong></p></td>
<td align="left"><p>最少16位 <strong>ebp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sp</strong></p></td>
<td align="left"><p>低16位 <strong>esp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>fc-al</strong></p></td>
<td align="left"><p>低8位 <strong>eax</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>啊</strong></p></td>
<td align="left"><p><strong>Ax</strong>的高8位</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bl</strong></p></td>
<td align="left"><p>低8位 <strong>ebx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bh</strong></p></td>
<td align="left"><p>高8位 <strong>bx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cl</strong></p></td>
<td align="left"><p>低8位 <strong>ecx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>48</strong></p></td>
<td align="left"><p>8位 <strong>cx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>磁盘</strong></p></td>
<td align="left"><p>低8位 <strong>edx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dh</strong></p></td>
<td align="left"><p><strong>Dx</strong>的高8位</p></td>
</tr>
</tbody>
</table>

 

对 subregister 的操作只会影响 subregister，而不会影响 subregister 以外的部分。 例如，存储到 **ax** 寄存器会使 **eax** 寄存器的高16位保持不变。

使用 [**？ (计算 Expression) **](---evaluate-expression-.md) 命令时，寄存器应以 "at" 符号 ( ) 为前缀 **@** 。 例如，你应该使用<strong> @ax ？</strong>而不是 **？ ax**。 这可确保调试器将 **ax** 识别为寄存器，而不是符号。

但是， [**r (寄存器) **](r--registers-.md) 命令中不需要 ( @ ) 。 例如， **r ax = 5** 将始终正确解释。

其他两个寄存器对于处理器的当前状态很重要。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>eip</strong></p></td>
<td align="left"><p>指令指针</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>flag</strong></p></td>
<td align="left"><p>flags</p></td>
</tr>
</tbody>
</table>

 

指令指针是要执行的指令的地址。

标志注册是一组单一位标志。 许多说明会改变标志来描述指令的结果。 然后，可以通过条件跳转说明测试这些标志。 有关详细信息，请参阅 [X86 标志](#x86-flags) 。

### <a name="span-idcalling_conventionsspanspan-idcalling_conventionsspanspan-idcalling_conventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>调用约定

X86 体系结构具有多个不同的调用约定。 幸运的是，它们都遵循相同的寄存器保留和函数返回规则：

-   函数必须保留所有寄存器， **eax**、 **ecx**和 **edx**除外，可以在函数调用中更改这些寄存器 **，并且必须**根据调用约定对其进行更新。

-   如果结果为32位或更小，则 **eax** 寄存器接收函数返回值。 如果结果为64位，则结果存储在 **edx： eax** 对中。

下面是用于 x86 体系结构的调用约定的列表：

-   Win32 (** \_ \_ stdcall**) 

    函数参数在堆栈上传递，从右到左推送，被调用方清理堆栈。

-   本机 c + + 方法调用 (也称为 thiscall) 

    函数参数将在堆栈上传递，从右到左推送，在 **ecx** 寄存器中传递 "this" 指针，被调用方清理堆栈。

-   C + + 方法调用的 COM (** \_ \_ stdcall**) 

    函数参数在堆栈上传递，从右到左，然后将 "this" 指针推送到堆栈上，然后调用函数。 被调用方清理堆栈。

-   **\_\_fastcall**

    在 **ecx** 和 **edx** 寄存器中传递前两个 DWORD 或更小的参数。 剩余的参数在堆栈上传递（从右到左）。 被调用方清理堆栈。

-   **\_\_cdecl**

    函数参数在堆栈上传递，从右到左推送，并且调用方清理堆栈。 ** \_ \_ Cdecl**调用约定用于具有可变长度参数的所有函数。

### <a name="span-iddebugger_display_of_registers_and_flagsspanspan-iddebugger_display_of_registers_and_flagsspanspan-iddebugger_display_of_registers_and_flagsspandebugger-display-of-registers-and-flags"></a><span id="Debugger_Display_of_Registers_and_Flags"></span><span id="debugger_display_of_registers_and_flags"></span><span id="DEBUGGER_DISPLAY_OF_REGISTERS_AND_FLAGS"></span>调试器显示寄存器和标志

下面是一个示例调试器寄存器显示：

```dbgcmd
eax=00000000 ebx=008b6f00 ecx=01010101 edx=ffffffff esi=00000000 edi=00465000
eip=77f9d022 esp=05cffc48 ebp=05cffc54 iopl=0         nv up ei ng nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000286
```

在用户模式调试中，可以忽略 **iopl** 和调试器显示的整个最后一行。

### <a name="span-idx86-flagsspanspan-idx86_flagsspanx86-flags"></a><span id="x86-flags"></span><span id="X86_FLAGS"></span>x86 标志

在前面的示例中，第二行末尾的双字母代码是 *标志*。 这些都是单数位寄存器，并且有多种用途。

下表列出了 x86 标志：

标志代码标志名称值标志 **状态说明**

溢出标志

0 1 **nvov**

无溢出溢出 **df**

方向标志

0 1 **updn**

**如果**

中断标志

0 1 **diei**

中断已禁用中断启用 **sf**

签名标志

0 1 **plng**

正 (或零) 负 **zf**

零标志

0 1 **nzzr**

非零零 **af**

辅助携带标志

0 1 **naac**

无辅助执行辅助传输 **pf**

奇偶校验标志

0 1 **pepo**

奇偶校验奇偶校验偶 **cf**

携带标志

0 1 **nccy**

No 携带 **tf**

陷阱标志

如果 **tf** 等于1，则在 \_ \_ 执行一条指令后，处理器将引发单步骤异常状态。 调试器使用此标志来实现单步跟踪。 它不应被其他应用程序使用。

**iopl**

I/o 特权级别

这是一个2位整数，其值介于0和3之间。 操作系统使用它来控制对硬件的访问。 应用程序不应使用此方法。

 

当寄存器作为某些命令在调试器命令窗口中显示时，将显示 " *标记状态* "。 但是，如果想要使用 [**r (寄存器) **](r--registers-.md) 命令更改标志，则应通过 *标记代码*对其进行引用。

在 WinDbg 的 "寄存器" 窗口中，标志代码用于查看或更改标志。 不支持标志状态。

示例如下。 在上述寄存器显示中，将显示标志状态 " **ng** "。 这意味着符号标志当前设置为1。 若要更改此项，请使用以下命令：

```dbgcmd
r sf=0
```

这会将符号标志设置为零。 如果执行其他注册，则不会显示 " **ng** " 状态代码。 相反，将显示 **pl** 状态代码。

符号标志、零标志和携带标志是最常用的标志。

### <a name="span-idconditionsspanspan-idconditionsspanspan-idconditionsspanconditions"></a><span id="Conditions"></span><span id="conditions"></span><span id="CONDITIONS"></span>条件和条款

描述一个或多个标志的状态的 *条件* 。 X86 上的所有条件操作都以条件表示。

汇编程序使用一个或两个字母缩写来表示条件。 可以用多个缩写来表示条件。 例如，AE ( "以上" 或 "等于" ) 与 NB ( "不低于" ) 。 下表列出了一些常见条件及其含义。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条件名称</th>
<th align="left">Flags</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Z</p></td>
<td align="left"><p>ZF = 1</p></td>
<td align="left"><p>上次操作的结果为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NZ</p></td>
<td align="left"><p>ZF = 0</p></td>
<td align="left"><p>上次操作的结果不是零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>C</p></td>
<td align="left"><p>CF = 1</p></td>
<td align="left"><p>上次操作要求具有 "执行" 或 "借用"。  (无符号整数，表示溢出。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>NC</p></td>
<td align="left"><p>CF = 0</p></td>
<td align="left"><p>最后一道工序不需要带有或借用的。  (无符号整数，表示溢出。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>SF = 1</p></td>
<td align="left"><p>上次操作的结果设置了其高位。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS</p></td>
<td align="left"><p>SF = 0</p></td>
<td align="left"><p>上次操作的结果是其高清晰。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>O</p></td>
<td align="left"><p>Of = 1</p></td>
<td align="left"><p>当被视为带符号的整数运算时，最后一个操作导致溢出或下溢。</p></td>
</tr>
<tr class="even">
<td align="left"><p>是</p></td>
<td align="left"><p>Of = 0</p></td>
<td align="left"><p>当被视为带符号整数运算时，最后一个操作不会导致溢出或下溢。</p></td>
</tr>
</tbody>
</table>

 

还可以使用条件来比较两个值。 **Cmp**指令比较了两个操作数，然后设置了标志，就像从另一个操作数中减去一个操作数一样。 以下条件可用于检查 **cmp** *value1*， *value2*的结果。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条件名称</th>
<th align="left">Flags</th>
<th align="left">表示 CMP 操作之后的。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>ZF = 1</p></td>
<td align="left"><p><em>value1</em>  == <em>value2</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NE</p></td>
<td align="left"><p>ZF = 0</p></td>
<td align="left"><p><em>value1</em> ！ = <em>value2</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
GE NL</td>
<td align="left"><p>SF = OF</p></td>
<td align="left"><p></p>
<em>value1</em> &gt; value1 = <em>value2</em>。
值被视为有符号整数。</td>
</tr>
<tr class="even">
<td align="left"><p></p>
LE NG</td>
<td align="left"><p>ZF = 1 或 SF！ = of</p></td>
<td align="left"><p><em>value1</em> &lt; value1 = <em>value2</em>。 值被视为有符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
G NLE</td>
<td align="left"><p>ZF = 0，SF = of</p></td>
<td align="left"><p><em>value1</em> &gt;<em>value2</em>。 值被视为有符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
L NGE</td>
<td align="left"><p>SF！ = OF</p></td>
<td align="left"><p><em>value1</em> &lt;<em>value2</em>。 值被视为有符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
AE NB</td>
<td align="left"><p>CF = 0</p></td>
<td align="left"><p><em>value1</em> &gt; value1 = <em>value2</em>。 值被视为无符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
为 NA</td>
<td align="left"><p>CF = 1 或 ZF = 1</p></td>
<td align="left"><p><em>value1</em> &lt; value1 = <em>value2</em>。 值被视为无符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
N</td>
<td align="left"><p>CF = 0，ZF = 0</p></td>
<td align="left"><p><em>value1</em> &gt;<em>value2</em>。 值被视为无符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
B NAE</td>
<td align="left"><p>CF = 1</p></td>
<td align="left"><p><em>value1</em> &lt;<em>value2</em>。 值被视为无符号整数。</p></td>
</tr>
</tbody>
</table>

 

条件通常用于处理 **cmp** 或 **测试** 指令的结果。 例如，

```asm
cmp eax, 5
jz equal
```

通过计算 (**eax** -5) 的表达式并根据结果设置标志来比较**eax**寄存器是否为数字5。 如果减法的结果为零，则将设置 **zr** 标志，并且 **jz** 条件将为 true，因此将执行跳转。

### <a name="span-iddata_typesspanspan-iddata_typesspanspan-iddata_typesspandata-types"></a><span id="Data_Types"></span><span id="data_types"></span><span id="DATA_TYPES"></span>数据类型

-   字节：8位

-   word：16位

-   dword：32位

-   qword：64位 (包含浮点双精度) 

-   tword：80位 (包含浮点扩展双精度) 

-   oword：128位

### <a name="span-idnotationspanspan-idnotationspanspan-idnotationspannotation"></a><span id="Notation"></span><span id="notation"></span><span id="NOTATION"></span>图解

下表指示用于描述汇编语言说明的表示法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表示法</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>r</strong>、 <strong>r1</strong>、 <strong>r2</strong>.。。</p></td>
<td align="left"><p>寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>内存地址 (有关详细信息，请参阅 "后续寻址模式" 部分。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>#n</p></td>
<td align="left"><p>立即常量</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>寄存器或内存</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r</strong>/#n</p></td>
<td align="left"><p>注册或立即常量</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>Register、memory 或 immediate 常量</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>cc</em></p></td>
<td align="left"><p>上述条件部分中列出的条件代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>T</em></p></td>
<td align="left"><p>"B"、"W" 或 "D" (字节、字或 dword) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>acc<em>T</em></p></td>
<td align="left"><p>大小<em>为</em>"累加器<strong>"：如果</strong> <em>t</em> = "B"，则<strong>ax</strong> if <em>t</em> = "W"，或者如果<em>t</em> = "D"，则为<strong>eax</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idaddressing_modesspanspan-idaddressing_modesspanspan-idaddressing_modesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>寻址模式

有几种不同的寻址模式，但它们都采用**t ptr \[ expr \] **格式，其中**t**是某些数据类型 (请参阅前面的数据类型部分) 而**expr**是涉及常量和寄存器的表达式。

大多数模式的表示法可能不太困难。 例如，**字节 PTR \[ esi + edx \* 8 + 3 \] **表示 "获取**esi**寄存器的值，将**edx**寄存器值的8倍添加到该寄存器中，添加三个，然后访问生成的地址处的字节。"

### <a name="span-idpipeliningspanspan-idpipeliningspanspan-idpipeliningspanpipelining"></a><span id="Pipelining"></span><span id="pipelining"></span><span id="PIPELINING"></span>传送

Pentium 是双重问题，这意味着它可以在一个时钟周期内最多执行两个操作。 不过，一次能够同时执行两个操作 (称为 *配对*) 的规则非常复杂。

由于 x86 是 CISC 的处理器，因此不必担心跳过延迟槽。

### <a name="span-idsynchronized_memory_accessspanspan-idsynchronized_memory_accessspanspan-idsynchronized_memory_accessspansynchronized-memory-access"></a><span id="Synchronized_Memory_Access"></span><span id="synchronized_memory_access"></span><span id="SYNCHRONIZED_MEMORY_ACCESS"></span>同步内存访问

"加载"、"修改" 和 "存储" 指令可接收一个 **锁** 前缀，该前缀用于修改说明，如下所示：

1.  发出指令之前，CPU 将刷新所有挂起的内存操作以确保一致性。 放弃所有数据预提取。

2.  发出指令时，CPU 将具有对总线的独占访问权限。 这可确保加载/修改/存储操作的原子性。

**Xchg**指令会在它与内存交换值时自动服从前面的规则。

所有其他说明默认为 nonlocking。

### <a name="span-idjump_predictionspanspan-idjump_predictionspanspan-idjump_predictionspanjump-prediction"></a><span id="Jump_Prediction"></span><span id="jump_prediction"></span><span id="JUMP_PREDICTION"></span>跳转预测

预测跳跃跳跃。

根据条件跳转是在上次执行时执行，还是不采取条件跳转。 记录跳跃历史记录的缓存大小受到限制。

如果 CPU 没有一条记录，指出是在上次执行条件跳转时还是不执行该操作，则它会根据所采用的方式预测后向条件跳转，并将其转发到不采用的条件。

### <a name="span-idalignmentspanspan-idalignmentspanspan-idalignmentspanalignment"></a><span id="Alignment"></span><span id="alignment"></span><span id="ALIGNMENT"></span>关联

X86 处理器会自动更正未对齐的内存访问，同时降低性能。 不引发异常。

如果地址是对象大小的整数倍，则内存访问被视为对齐。 例如，所有字节访问都是对齐的， (所有内容都是 1) 的整数倍，即使地址是相同的，也是如此，即使地址是相同的，DWORD 地址也必须是4的倍数才能对齐。

不应将 **锁** 前缀用于未对齐的内存访问。

 

 





