---
title: MASM 数字和运算符
description: MASM 数字和运算符
ms.assetid: 9aeb3ef2-d83a-4f99-9a55-4bbd8a7e11b5
keywords:
- 表达式中，MASM 表达式语法
- 数值表达式 (MASM)
- 数字的 MASM 表达式
- MASM 表达式、 运算符
- 运算符 (MASM)
- （MASM 前缀）
- 二元运算符
- 移位运算符
- 一元运算符
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9890f3cae44d4c232876eb0cb4a498d400974e32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363420"
---
# <a name="masm-numbers-and-operators"></a>MASM 数字和运算符


## <span id="ddk_masm_numbers_and_operators_dbg"></span><span id="DDK_MASM_NUMBERS_AND_OPERATORS_DBG"></span>


在 4.0 版的 Windows 调试工具软件包之前, NTSD、 CDB、 KD 和 WinDbg 使用仅 Microsoft Macro Assembler (MASM) 的表达式语法。

### <a name="span-idnumbersinmasmexpressionsspanspan-idnumbersinmasmexpressionsspannumbers-in-masm-expressions"></a><span id="numbers_in_masm_expressions"></span><span id="NUMBERS_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的数字

可以将数字放在基 16、 10、 8 或 2 的 MASM 表达式中。

使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令，将默认基数为 16、 10 或 8。 然后此基中解释没有前缀的所有数字。 可以通过指定重写默认基数**0x**前缀 （十六进制） **0n**前缀 （十进制） **0t**前缀 （八进制） 或**0y**前缀 （二进制）。

此外可以通过添加指定十六进制数字**h**数后。 可以使用大写或小写字母数字中。 例如，"0x4AB3"、"0X4aB3"，"4AB3h"、"4ab3h"和"4aB3H"具有相同的含义。

如果不在表达式中的前缀后添加一个数字，是读取数为 0。 因此，您可以为 0 时，前缀后跟 0，并且仅前缀编写 0。 例如，以十六进制格式，"0"、"0x0"和"0x"具有相同的含义。

可以输入中的十六进制 64 位值**xxxxxxxx\`xxxxxxxx**格式。 也可以省略重读符号 (\`)。 如果包括抑音符[自动符号扩展](sign-extension.md)被禁用。

### <a name="span-idsymbolsinmasmexpressionsspanspan-idsymbolsinmasmexpressionsspansymbols-in-masm-expressions"></a><span id="symbols_in_masm_expressions"></span><span id="SYMBOLS_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的符号

MASM 表达式中任何符号的数字值是其内存地址。 具体取决于符号所引用的内容，此地址是全局变量、 本地变量、 函数、 段、 模块或任何其他可识别的标签的地址。

若要指定的地址是与相关联的模块，包括模块名称和感叹号 （！） 的符号名称之前。 如果该符号可以解释为十六进制数，包括模块名称和感叹点或只是感叹号符号名称前。 有关符号识别的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

使用两个冒号 （:）或两个下划线 (\_\_) 以指示类的成员。

使用重读音符 (\`) 或撇号 （'） 中的符号名称只有在添加的模块名称和感叹号符号之前。

### <a name="span-idnumericoperatorsinmasmexpressionsspanspan-idnumericoperatorsinmasmexpressionsspannumeric-operators-in-masm-expressions"></a><span id="numeric_operators_in_masm_expressions"></span><span id="NUMERIC_OPERATORS_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的数字运算符

使用一元运算符，可以修改的表达式的任何组件。 使用二元运算符，可以组合任意两个组件。 一元运算符优先于二元运算符。 当使用多个二元运算符时，运算符将遵循以下表中所述的固定的优先顺序规则。

您始终可以使用括号替代优先顺序规则。

如果 MASM 表达式的一部分括在括号中，并且两个 at 符号 （@ @） 出现在表达式之前，该表达式将解释根据[C++表达式规则](c---numbers-and-operators.md)。 无法添加这两个 at 符号和左括号之间有空格。 此外可以指定[表达式计算器](evaluating-expressions.md)通过使用 **@@c+ + （...）** 或 **@@masm（...）**.

当你执行算术运算时，MASM 表达式计算器将所有数字和符号视为 ULONG64 类型。

一元地址运算符假设地址的默认段为 DS。 运算符优先级的顺序计算表达式。 如果相邻的运算符具有相同的优先级，计算表达式从左到右。

可以使用下列一元运算符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">运算符</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>+</p></td>
<td align="left"><p>一元加</p></td>
</tr>
<tr class="even">
<td align="left"><p>-</p></td>
<td align="left"><p>一元负</p></td>
</tr>
<tr class="odd">
<td align="left"><p>非</p></td>
<td align="left"><p>如果参数为零，则返回 1。 任何非零值的参数，则返回零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>hi</strong></p></td>
<td align="left"><p>高 16 位</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>low</strong></p></td>
<td align="left"><p>低 16 位</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>by</strong></p></td>
<td align="left"><p>从指定的地址的低序位字节。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pby</strong></p></td>
<td align="left"><p>与相同<strong>通过</strong>，但前者的物理地址。 可以读取仅使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wo</strong></p></td>
<td align="left"><p>从指定的地址的低序位字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pwo</strong></p></td>
<td align="left"><p>与相同<strong>wo</strong> ，但前者的物理地址。 可以读取仅使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dwo</strong></p></td>
<td align="left"><p>从指定的地址双字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pdwo</strong></p></td>
<td align="left"><p>与相同<strong>dwo</strong> ，但前者的物理地址。 可以读取仅使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>qwo</strong></p></td>
<td align="left"><p>从指定的地址四字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pqwo</strong></p></td>
<td align="left"><p>与相同<strong>qwo</strong> ，但前者的物理地址。 可以读取仅使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>poi</strong></p></td>
<td align="left"><p>从指定的地址指针大小的数据。 指针大小为 32 位或 64 位。 在内核调试，此大小基于的处理器<em>目标</em>计算机。 在用户模式下调试在基于 Itanium 的计算机上，此大小为 32 位或 64 位，具体取决于目标应用程序。 因此， <strong>poi</strong>是要使用如果你想指针大小的数据的最佳运算符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ppoi</strong></p></td>
<td align="left"><p>与相同<strong>poi</strong> ，但前者的物理地址。 可以读取仅使用默认缓存行为的物理内存。</p></td>
</tr>
</tbody>
</table>

 

可以使用以下二进制运算符。 每个单元格中的运算符优先于较小的单元中。 相同单元中的运算符均属于相同的优先级，从左到右进行分析。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">运算符</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>*</p>
<p>/</p>
<p><strong>mod</strong> （或 %）</p></td>
<td align="left"><p>乘法</p>
<p>整数除法</p>
<p>取模 （余数）</p></td>
</tr>
<tr class="even">
<td align="left"><p>+</p>
<p>-</p></td>
<td align="left"><p>添加</p>
<p>减法</p></td>
</tr>
<tr class="odd">
<td align="left"><p>&lt;&lt;</p>
<p>&gt;&gt;</p>
<p>&gt;&gt;&gt;</p></td>
<td align="left"><p>左的移</p>
<p>逻辑右移位</p>
<p>算术右移位运算</p></td>
</tr>
<tr class="even">
<td align="left"><p>= （或 = =）</p>
<p>&lt;</p>
<p>&gt;</p>
<p>&lt;=</p>
<p>&gt;=</p>
<p>!=</p></td>
<td align="left"><p>等于</p>
<p>小于</p>
<p>大于</p>
<p>小于或等于</p>
<p>大于或等于</p>
<p>不等于</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>并</strong>(或&amp;)</p></td>
<td align="left"><p>位与</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>xor</strong> (或 ^)</p></td>
<td align="left"><p>按位 XOR （异或）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>或</strong>(或 |)</p></td>
<td align="left"><p>按位 OR 运算符</p></td>
</tr>
</tbody>
</table>

 

&lt;， &gt;、 =、 = =、 和 ！ = 的比较运算符计算结果为 1，如果表达式为 true 或为零，如果表达式为 false。 单个等号 （=） 是双等号 （= =） 相同。 不能使用副作用或 MASM 表达式中的分配。

在"操作数错误"中无效的操作 （如被零除） 结果返回到[调试器命令窗口](debugger-command-window.md)。

### <a name="span-idnonnumericoperatorsinmasmexpressionsspanspan-idnonnumericoperatorsinmasmexpressionsspannon-numeric-operators-in-masm-expressions"></a><span id="non_numeric_operators_in_masm_expressions"></span><span id="NON_NUMERIC_OPERATORS_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的非数字运算符

此外可以在 MASM 表达式中使用以下其他运算符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">运算符</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$fnsucc(</strong><em>FnAddress</em>, <em>RetVal</em>, <em>Flag</em><strong>)</strong></p></td>
<td align="left"><p>解释<em>RetVal</em>位于函数的返回值的值<em>FnAddress</em>地址。 如果此返回值被返回成功代码，称为<strong>$fnsucc</strong>返回<strong>TRUE</strong>。 否则为<strong>$fnsucc</strong>返回<strong>FALSE</strong>。</p>
<p>如果返回类型为布尔值、 bool、 句柄、 HRESULT 或 NTSTATUS， <strong>$fnsucc</strong>正确理解是否在指定的返回值被称为成功代码。 返回类型是否为指针，所有值，而<strong>NULL</strong>才会被视为成功代码。 成功的值对于任何其他类型进行定义<em>标志</em>。 如果<em>标志</em>为 0，一个非零值的<em>RetVal</em>为 success。 如果<em>标志</em>为 1，零值的<em>RetVal</em>为 success。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$iment (</strong><em>地址</em><strong>)</strong></p></td>
<td align="left"><p>加载的模块列表中返回映像入口点的地址。 <em>地址</em>指定的可移植可执行文件 (PE) 映像基址。 通过查找映像的 PE 映像标头中的映像入口点找到该项，<em>地址</em>指定。</p>
<p>您可以使用此函数的是已在模块列表中，并设置这两个模块<a href="unresolved-breakpoints---bu-breakpoints-.md" data-raw-source="[unresolved breakpoints](unresolved-breakpoints---bu-breakpoints-.md)">无法解析的断点</a>通过使用<strong><a href="bp--bu--bm--set-breakpoint-.md" data-raw-source="[bu](bp--bu--bm--set-breakpoint-.md)">bu</a></strong>命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scmp("</strong><em>String1</em><strong>", "</strong><em>String2</em><strong>")</strong></p></td>
<td align="left"><p>计算结果为-1、 0 或 1，如<strong>strcmp</strong> C 函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$sicmp("</strong><em>String1</em><strong>", "</strong><em>String2</em><strong>")</strong></p></td>
<td align="left"><p>计算结果为-1、 0 或 1，如<strong>stricmp</strong> Microsoft Win32 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$spat("</strong><em>String</em><strong>", "</strong><em>Pattern</em><strong>")</strong></p></td>
<td align="left"><p>计算结果为<strong>，则返回 TRUE</strong>或<strong>FALSE</strong>取决于是否<em>字符串</em>匹配<em>模式</em>。 匹配不区分大小写。 <em>模式</em>可以包含各种通配符和说明符。 有关语法的详细信息，请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$vvalid(</strong><em>Address</em><strong>,</strong> <em>Length</em><strong>)</strong></p></td>
<td align="left"><p>确定是否内存范围的开始处<em>地址</em>，并为扩展<em>长度</em>字节是否有效。 如果有效，内存<strong>$vvalid</strong>的计算结果为 1。 如果内存是无效的<strong>$vvalid</strong>计算结果为 0。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idregistersandpseudoregistersinmasmexpressionsspanspan-idregistersandpseudoregistersinmasmexpressionsspanregisters-and-pseudo-registers-in-masm-expressions"></a><span id="registers_and_pseudo_registers_in_masm_expressions"></span><span id="REGISTERS_AND_PSEUDO_REGISTERS_IN_MASM_EXPRESSIONS"></span>寄存器和伪寄存器中的 MASM 表达式

可以使用寄存器和伪寄存器中的 MASM 表达式。 您可以添加 at 符号 (@) 之前所有寄存器和伪寄存器。 At 符号会使调试器能够更快地访问值。 在登录这不是必需的最常见的基于 x86 的寄存器。 有关其他寄存器和伪寄存器，我们建议您添加 at 符号，但并不真正需要。 如果省略不太常见的寄存器的符号，调试器会尝试分析的文本为十六进制数字，然后作为一个符号，最后为寄存器。

此外可以使用句点 （.） 以指示当前指令指针。 不应将添加在登录之前此段，并且您不能使用一段的第一个参数作为[ **r 命令**](r--registers-.md)。 此时间段与具有相同含义 **$ip**伪寄存器。

有关寄存器和伪寄存器的详细信息，请参阅[注册语法](register-syntax.md)并[伪寄存器语法](pseudo-register-syntax.md)。

### <a name="span-idsourcelinenumbersinmasmexpressionsspanspan-idsourcelinenumbersinmasmexpressionsspansource-line-numbers-in-masm-expressions"></a><span id="source_line_numbers_in_masm_expressions"></span><span id="SOURCE_LINE_NUMBERS_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的源行号

可以使用源代码文件和行号中的表达式的 MASM 表达式。 必须将这些表达式使用抑音符 (\`)。 有关语法的详细信息，请参阅[源行语法](source-line-syntax.md)。

 

 





