---
title: x86 体系结构
description: x86 体系结构
ms.assetid: 42c62647-7c9a-496e-839f-91283db73a29
keywords:
- x86 处理器，体系结构
- 寄存器，x86 处理器
- x86 处理器，注册
- x86 处理器，调用约定
- x86 处理器，数据类型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7da158a055960451e60d2275f2b26333db1fadc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381915"
---
# <a name="x86-architecture"></a>x86 体系结构


## <span id="ddk_x86_architecture_dbg"></span><span id="DDK_X86_ARCHITECTURE_DBG"></span>


Intel x86 处理器使用复杂的指令集计算机 (CISC) 体系结构，这意味着数量适中的专用寄存器，而不是大量的通用寄存器。 这还意味着将 predominate 复杂的特殊用途说明。

X86 处理器跟踪在其遗产至少尽量回复为 8 位 Intel 8080 处理器。 在 x86 指令集是由于向后兼容性与该处理器 （和其 Zilog Z-80 变体） 中的很多失望。

在 Microsoft Win32 使用 x86 处理器*32 位平面模式*。 本文档将仅重点平面模式。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>注册

X86 体系结构包括以下无特权整数寄存器。

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
<td align="left"><p>计数器寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>edx</strong></p></td>
<td align="left"><p>数据寄存器-可用于 I/O 端口的访问和算术函数</p></td>
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
<td align="left"><p><strong>esp</strong></p></td>
<td align="left"><p>堆栈指针</p></td>
</tr>
</tbody>
</table>

 

32 位的所有整数寄存器。 但是，很多具有 16 位或 8 位 subregisters。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ax</strong></p></td>
<td align="left"><p>低 16 位的<strong>eax</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bx</strong></p></td>
<td align="left"><p>低 16 位的<strong>ebx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cx</strong></p></td>
<td align="left"><p>低 16 位的<strong>ecx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dx</strong></p></td>
<td align="left"><p>低 16 位的<strong>edx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p>低 16 位的<strong>esi</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>di</strong></p></td>
<td align="left"><p>低 16 位的<strong>edi</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bp</strong></p></td>
<td align="left"><p>低 16 位的<strong>ebp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sp</strong></p></td>
<td align="left"><p>低 16 位的<strong>esp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>al</strong></p></td>
<td align="left"><p>低 8 位的<strong>eax</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ah</strong></p></td>
<td align="left"><p>高 8 位<strong>ax</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bl</strong></p></td>
<td align="left"><p>低 8 位的<strong>ebx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bh</strong></p></td>
<td align="left"><p>高 8 位<strong>bx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cl</strong></p></td>
<td align="left"><p>低 8 位的<strong>ecx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ch</strong></p></td>
<td align="left"><p>高 8 位<strong>cx</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dl</strong></p></td>
<td align="left"><p>低 8 位的<strong>edx</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dh</strong></p></td>
<td align="left"><p>高 8 位<strong>dx</strong></p></td>
</tr>
</tbody>
</table>

 

对 subregister 操作会影响仅 subregister 和 none 外 subregister 部分。 例如，存储到**ax**寄存器离开高 16 位**eax**注册保持不变。

使用时[ **？（计算表达式）** ](---evaluate-expression-.md)命令时，应使用"at"符号作为前缀寄存器 ( **@** )。 例如，应使用<strong>？@ax</strong> 而非 **？ ax**。 这可确保调试器能够识别**ax**作为一个函数注册表，而不是一个符号。

但是，(@) 中不需要[ **r （寄存器）** ](r--registers-.md)命令。 例如， **r ax = 5**始终正确解释。

重要的处理器的当前状态的两个其他寄存器。

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
<td align="left"><p><strong>flags</strong></p></td>
<td align="left"><p>标志</p></td>
</tr>
</tbody>
</table>

 

指令指针位于正在执行的指令的地址。

标志注册是一个位标志的集合。 许多指令更改的标志来描述指令的结果。 然后可以按条件跳转指令测试这些标志。 请参阅[x86 标志](#x86-flags)有关详细信息。

### <a name="span-idcallingconventionsspanspan-idcallingconventionsspanspan-idcallingconventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>调用约定

X86 体系结构具有多个不同的调用约定。 幸运的是，它们都遵循相同的注册保留和函数返回规则：

-   函数必须保留所有寄存器除外**eax**， **ecx**，并**edx**，这可以在函数调用之间更改和**esp**，这必须更新根据调用约定。

-   **Eax**注册接收函数返回值，如果结果为 32 位或更小。 如果结果为 64 位，则结果存储在**edx: eax**对。

以下是一系列调用约定使用 x86 体系结构：

-   Win32 ( **\_\_stdcall**)

    直接推送到左侧，在堆栈上传递的函数参数和被调用方清理堆栈。

-   本机C++方法调用 (也称为 thiscall)

    从左到右推送到堆栈上传递的函数参数，"this"指针传入**ecx**和被调用方清理堆栈。

-   COM ( **\_\_stdcall**为C++方法调用)

    函数参数传递到堆栈上，推送右到左，然后"this"指针推送到堆栈上，然后调用该函数。 被调用方清理堆栈。

-   **\_\_fastcall**

    前两个 DWORD 或小参数中传递**ecx**并**edx**注册。 其余参数从左到右推送到堆栈上传递。 被调用方清理堆栈。

-   **\_\_cdecl**

    直接推送到左侧，在堆栈上传递的函数参数和调用方清理堆栈。 **\_\_Cdecl**调用约定用于使用长度可变的参数的所有功能。

### <a name="span-iddebuggerdisplayofregistersandflagsspanspan-iddebuggerdisplayofregistersandflagsspanspan-iddebuggerdisplayofregistersandflagsspandebugger-display-of-registers-and-flags"></a><span id="Debugger_Display_of_Registers_and_Flags"></span><span id="debugger_display_of_registers_and_flags"></span><span id="DEBUGGER_DISPLAY_OF_REGISTERS_AND_FLAGS"></span>调试器显示的寄存器和标志

下面是示例调试器注册显示：

```dbgcmd
eax=00000000 ebx=008b6f00 ecx=01010101 edx=ffffffff esi=00000000 edi=00465000
eip=77f9d022 esp=05cffc48 ebp=05cffc54 iopl=0         nv up ei ng nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000286
```

在用户模式调试中，您可以忽略**iopl**和调试器显示的整个最后一行。

### <a name="span-idx86-flagsspanspan-idx86flagsspanx86-flags"></a><span id="x86-flags"></span><span id="X86_FLAGS"></span>x86 标志

在上述示例中，在第二行末尾的双字母代码都*标志*。 这是单一位寄存器，有多种用途。

下表列出了 x86 标志：

标记代码标志名称值标志状态状态说明**的**

溢出标志

0 1 **nvov**

无溢出溢出**df**

方向标志

0 1 **updn**

方向向上方向向下**如果**

中断标志

0 1 **diei**

中断禁用已启用的中断**sf**

符号标志

0 1 **plng**

正 （或零） 负**zf**

零个标志

0 1 **nzzr**

Nonzero Zero **af**

辅助携带标志

0 1 **naac**

没有辅助执行辅助携带**pf**

奇偶校验标志

0 1 **pepo**

奇偶校验偶校验奇数**cf**

执行标志

0 1 **nccy**

没有携带携带**tf**

陷阱标志

如果**tf**等于 1 时，处理器将引发状态\_单个\_后的一条指令执行的步骤例外。 由调试器使用此标志来实现单步执行跟踪。 它不应使用由其他应用程序。

**iopl**

I/O 权限级别

这是一个 two-bit 整数，其值介于 0 和 3。 操作系统使用它来控制对硬件的访问。 它不应由应用程序使用。

 

当在调试器命令窗口中的某些命令的结果显示寄存器时，它是*标志状态*显示。 但是，如果你想要更改标志使用[ **r （寄存器）** ](r--registers-.md)命令时，应通过参考*标记代码*。

在 WinDbg 寄存器窗口中，标志代码用于查看或更改标志。 不支持标志状态。

下面是一个示例。 在前面注册显示标志状态**ng**出现。 这意味着符号标志当前设置为 1。 若要更改此设置，请使用以下命令：

```dbgcmd
r sf=0
```

这将符号标志设置为零。 如果另一个寄存器显示，这样做**ng**状态代码将不会出现。 相反， **pl**将显示状态代码。

符号标志、 零标志和执行标志是最常用的标志。

### <a name="span-idconditionsspanspan-idconditionsspanspan-idconditionsspanconditions"></a><span id="Conditions"></span><span id="conditions"></span><span id="CONDITIONS"></span>条件

一个*条件*描述的一个或多个标志的状态。 条件以表示在 x86 上的所有条件操作。

在组装器使用一个或两个字母缩写形式来表示一个条件。 可以由多个缩写表示一个条件。 例如，AE （"更高版本或等于"） 是为 NB （"不下面"） 相同的条件。 下表列出了一些常见情形和及其含义。

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
<td align="left"><p>ZF=1</p></td>
<td align="left"><p>最后一个操作的结果为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NZ</p></td>
<td align="left"><p>ZF=0</p></td>
<td align="left"><p>最后一个操作的结果不为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>C</p></td>
<td align="left"><p>CF=1</p></td>
<td align="left"><p>最后一次操作所需执行或借用。 （对于无符号整数，这指示溢出。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>NC</p></td>
<td align="left"><p>CF=0</p></td>
<td align="left"><p>最后一次操作没有要求进位或借用。 （对于无符号整数，这指示溢出。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>SF=1</p></td>
<td align="left"><p>最后一次操作的结果具有其高的位设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS</p></td>
<td align="left"><p>SF=0</p></td>
<td align="left"><p>最后一个操作的结果都有其高的位清除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>O</p></td>
<td align="left"><p>OF=1</p></td>
<td align="left"><p>当被视为带符号的整数操作，最后一个操作将导致溢出或下溢。</p></td>
</tr>
<tr class="even">
<td align="left"><p>否</p></td>
<td align="left"><p>OF=0</p></td>
<td align="left"><p>当被视为带符号的整数操作，最后一次操作未不会导致溢出或下溢。</p></td>
</tr>
</tbody>
</table>

 

此外可以使用条件来比较两个值。 **Cmp**指令将两个操作数，进行比较，然后设置标志，就像从另一个操作数中减去。 可以使用以下条件检查的结果**cmp** *value1*， *value2*。

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
<th align="left">这意味着 CMP 操作之后。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>ZF=1</p></td>
<td align="left"><p><em>value1</em> == <em>value2</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NE</p></td>
<td align="left"><p>ZF=0</p></td>
<td align="left"><p><em>value1</em> != <em>value2</em>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
GE NL</td>
<td align="left"><p>SF=OF</p></td>
<td align="left"><p></p>
<em>value1</em> &gt;= <em>value2</em>.
值被视为带符号整数。</td>
</tr>
<tr class="even">
<td align="left"><p></p>
LE NG</td>
<td align="left"><p>ZF=1 or SF!=OF</p></td>
<td align="left"><p><em>value1</em> &lt;= <em>value2</em>. 值被视为带符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
G NLE</td>
<td align="left"><p>ZF = 0 和 SF = OF</p></td>
<td align="left"><p><em>value1</em> &gt; <em>value2</em>。 值被视为带符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
L NGE</td>
<td align="left"><p>SF!=OF</p></td>
<td align="left"><p><em>value1</em> &lt; <em>value2</em>。 值被视为带符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
AE NB</td>
<td align="left"><p>CF=0</p></td>
<td align="left"><p><em>value1</em> &gt;= <em>value2</em>. 值被视为无符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
BE NA</td>
<td align="left"><p>CF = 1 或 ZF = 1</p></td>
<td align="left"><p><em>value1</em> &lt;= <em>value2</em>. 值被视为无符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
NBE</td>
<td align="left"><p>CF = 0 和 ZF = 0</p></td>
<td align="left"><p><em>value1</em> &gt; <em>value2</em>。 值被视为无符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
B NAE</td>
<td align="left"><p>CF=1</p></td>
<td align="left"><p><em>value1</em> &lt; <em>value2</em>。 值被视为无符号整数。</p></td>
</tr>
</tbody>
</table>

 

通常使用条件来执行操作的结果**cmp**或**测试**指令。 例如，

```asm
cmp eax, 5
jz equal
```

比较**eax**通过计算该表达式针对数字 5 注册 (**eax** -5) 和设置根据结果的标志。 如果该减法运算的结果为零，则**zr**将设置标志，并**jz**条件将为 true，因此不会采取跳转。

### <a name="span-iddatatypesspanspan-iddatatypesspanspan-iddatatypesspandata-types"></a><span id="Data_Types"></span><span id="data_types"></span><span id="DATA_TYPES"></span>数据类型

-   字节：8 位

-   word:16 位

-   dword:32 位

-   qword:64 位 （包括双精度浮点型）

-   tword:80 位 （包括浮点扩展的双精度型值）

-   oword:128 位

### <a name="span-idnotationspanspan-idnotationspanspan-idnotationspannotation"></a><span id="Notation"></span><span id="notation"></span><span id="NOTATION"></span>表示法

下表列出用于描述程序集语言指令的表示法。

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
<td align="left"><p><strong>r</strong>， <strong>r1</strong>， <strong>r2</strong>...</p></td>
<td align="left"><p>寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>内存地址 （请参阅后续的寻址模式部分，了解详细信息。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#n</p></td>
<td align="left"><p>即时常量</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>注册或内存</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r</strong>/#n</p></td>
<td align="left"><p>注册或即时常量</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>寄存器、 内存或即时常量</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>cc</em></p></td>
<td align="left"><p>在前面的条件部分中列出的条件代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>T</em></p></td>
<td align="left"><p>"B"、"W"或者"D"（字节、 字或双字节）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>acc<em>T</em></p></td>
<td align="left"><p>大小<em>T</em>累加器： <strong>al</strong>如果<em>T</em> ="B"， <strong>ax</strong>如果<em>T</em> ="W"或<strong>eax</strong>如果<em>T</em> ="D"</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idaddressingmodesspanspan-idaddressingmodesspanspan-idaddressingmodesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>寻址模式

有几个不同的寻址模式，但它们都需要在窗体**T ptr \[expr\]** ，其中**T**是一些数据类型 （请参阅前面的数据类型部分） 和**expr**是涉及常量和寄存器一些表达式。

大多数模式下的表示法可以推导内容。 例如，**字节 PTR \[esi + edx\*8 + 3\]** 意味着"采用的值**esi**注册、 向其添加值的八倍**edx**注册，添加三个，然后访问生成的地址处的字节。"

### <a name="span-idpipeliningspanspan-idpipeliningspanspan-idpipeliningspanpipelining"></a><span id="Pipelining"></span><span id="pipelining"></span><span id="PIPELINING"></span>流水线处理

Pentium 是双重的问题，这意味着它可以在一个时钟计时周期中执行最多两个操作。 但是上时能够同时执行两个操作, 的规则 (称为*配对*) 非常复杂。

X86 是 CISC 处理器，因为您无需担心跳转延迟槽。

### <a name="span-idsynchronizedmemoryaccessspanspan-idsynchronizedmemoryaccessspanspan-idsynchronizedmemoryaccessspansynchronized-memory-access"></a><span id="Synchronized_Memory_Access"></span><span id="synchronized_memory_access"></span><span id="SYNCHRONIZED_MEMORY_ACCESS"></span>同步的内存访问

加载、 修改和存储的说明可以接收**锁**前缀，这会修改指令，如下所示：

1.  之前发出指令，CPU 将刷新所有挂起的内存操作，以确保一致性。 将放弃所有数据预提取。

2.  同时发出指令，CPU 将具备到总线的独占访问权限。 这可确保加载/修改/存储操作的原子性。

**Xchg**指令自动遵循以前的规则，每当交换具有内存的值。

所有其他说明默认为 nonlocking。

### <a name="span-idjumppredictionspanspan-idjumppredictionspanspan-idjumppredictionspanjump-prediction"></a><span id="Jump_Prediction"></span><span id="jump_prediction"></span><span id="JUMP_PREDICTION"></span>跳转预测

预测采取无条件跳转。

预测条件跳转采用或所做的更改，具体取决于它们是否已执行的最后一次执行它们。 用于记录跳转历史记录缓存有大小限制。

如果 CPU 不具有条件跳转是否已采用或所做的更改已执行的最后一个时间的记录，它随着不再考虑预测条件的向后跳转，并转发作为不执行条件跳转。

### <a name="span-idalignmentspanspan-idalignmentspanspan-idalignmentspanalignment"></a><span id="Alignment"></span><span id="alignment"></span><span id="ALIGNMENT"></span>对齐方式

X86 处理器将自动更正未对齐的内存访问，在对性能产生负面影响。 不会引发异常。

内存访问被视为对齐的地址是一个整数，如果对象大小的倍数。 例如，对齐所有字节访问 (所有内容都是一个整数的倍数)、 都对齐 WORD 访问甚至地址和 DWORD 地址必须是为了都对齐 4 的倍数。

**锁**前缀不应该用于未对齐的内存访问。

 

 





