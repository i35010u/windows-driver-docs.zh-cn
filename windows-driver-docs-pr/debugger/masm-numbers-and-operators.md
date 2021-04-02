---
title: MASM 数字和运算符
description: MASM 数字和运算符
keywords:
- 表达式，MASM 表达式语法
- " (MASM) 的数值表达式"
- MASM 表达式，数值
- MASM 表达式，运算符
- '运算符 (MASM) '
- " (MASM 前缀) "
- 二元运算符
- 移位运算符
- 一元运算符
ms.date: 03/30/2021
ms.localizationpriority: medium
ms.openlocfilehash: a4d475406618f402047c2e3d23c07567956956fd
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113608"
---
# <a name="masm-numbers-and-operators"></a>MASM 数字和运算符

本主题介绍如何将 Microsoft 宏组装 (MASM) 表达式语法与 Windows 调试工具一起使用。

## <a name="numbers-in-debugger-masm-expressions"></a>调试器 MASM 表达式中的数字

可以在 base64、10、8或2中将数字放入 MASM 表达式中。

使用 [**n (Set Number Base)**](n--set-number-base-.md) 命令将默认基数设置为16、10或8。 然后，在此基准中解释所有没有前缀数字。 您可以通过指定 **0x** 前缀 (十六进制) 、 **0n** 前缀 (decimal) 、 **0t** 前缀 (八进制) 或 **w..1 ....** 前缀 (binary) 来覆盖默认基数。

还可以通过在数字后添加 **h** 来指定十六进制数。 可以在数字中使用大写或小写字母。 例如，"0x4AB3"、"0X4aB3"、"4AB3h"、"4AB3h" 和 "4aB3H" 的含义相同。

如果未在表达式中的前缀后面添加数字，则该数字将读取为0。 因此，你可以将0写入0，前缀后跟0，并且仅限前缀。 例如，在十六进制中，"0"、"0x0" 和 "0x" 的含义相同。

可以采用 **xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx \`** 格式输入十六进制64位值。 还可以省略) 的抑音符 (\` 。 如果包含 "抑音符"，则会禁用 [自动符号扩展](sign-extension.md) 。

## <a name="symbols-in-debugger-masm-expressions"></a>调试器 MASM 表达式中的符号

在 MASM 表达式中，任何符号的数字值都是它的内存地址。 根据符号引用的内容，此地址是全局变量、局部变量、函数、段、模块或任何其他可识别标签的地址。

若要指定与该地址关联的模块，请在符号名称之前包含模块名称和感叹号 (！ ) 。 如果符号可以解释为十六进制数，请在符号名之前包含模块名称和感叹号，或只包含一个惊叹号。 有关符号识别的详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

使用两个冒号 (：： ) 或两个下划线 (\_ \_) 来指示类的成员。

\`仅当在符号名称中添加了一个模块名称和感叹号时，才在符号名称中使用抑音符 () 或撇号 ( ") 。

## <a name="numeric-operators-in-masm-expressions"></a>MASM 表达式中的数字运算符

您可以通过使用一元运算符来修改表达式的任何组件。 可以通过使用二元运算符组合使用任意两个组件。 一元运算符优先于二元运算符。 当使用多个二元运算符时，运算符遵循下表中所述的固定优先规则。

始终可以使用括号覆盖优先规则。

如果将 MASM 表达式的一部分括在括号中，而两个 at 符号 ( @ @ ) 出现在表达式之前，则根据 [c + + 表达式规则](c---numbers-and-operators.md)解释该表达式。 不能在两个 at 符号和左括号之间添加空格。 还可以通过使用 **@ @c + + ( ... )** 或 **@ @masm ( ... )** 来指定 [表达式计算器](evaluating-expressions.md)。

执行算术计算时，MASM 表达式计算器会将所有数字和符号视为 ULONG64 类型。

一元地址运算符假设 DS 作为地址的默认段。 表达式按运算符优先级的顺序进行计算。 如果相邻运算符具有相等的优先级，则按从左至右的顺序计算表达式。

您可以使用以下一元运算符。

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
<td align="left"><p>not</p></td>
<td align="left"><p>如果参数为零，则返回1。 对于任何非零参数，返回零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>你好</strong></p></td>
<td align="left"><p>高16位</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>低级</strong></p></td>
<td align="left"><p>低16位</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>by</strong></p></td>
<td align="left"><p>来自指定地址的低序位字节。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pby</strong></p></td>
<td align="left"><p>与相同 <strong>，只不过它</strong> 使用物理地址。 只能读取使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wo</strong></p></td>
<td align="left"><p>指定地址中的低序位字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pwo</strong></p></td>
<td align="left"><p>与 <strong>wo</strong> 相同，只不过它使用物理地址。 只能读取使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dwo</strong></p></td>
<td align="left"><p>指定地址中的双字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pdwo</strong></p></td>
<td align="left"><p>与 <strong>dwo</strong> 相同，只不过它使用物理地址。 只能读取使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>qwo</strong></p></td>
<td align="left"><p>指定地址中的四字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pqwo</strong></p></td>
<td align="left"><p>与 <strong>qwo</strong> 相同，只不过它使用物理地址。 只能读取使用默认缓存行为的物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>poi</strong></p></td>
<td align="left"><p>指定地址中的指针大小的数据。 指针大小为32位或64位。 在内核调试中，此大小基于 <em>目标</em> 计算机的处理器。 因此，如果需要使用指针大小的数据， <strong>poi</strong> 是最佳运算符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ppoi</strong></p></td>
<td align="left"><p>与 <strong>poi</strong> 相同，只不过它使用物理地址。 只能读取使用默认缓存行为的物理内存。</p></td>
</tr>
</tbody>
</table>


您可以使用以下二元运算符。 每个单元中的运算符优先于位于较低单元格中的运算符。 相同单元中的运算符具有相同的优先级，并且是从左向右分析的。

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
<p><strong>mod</strong> (或% ) </p></td>
<td align="left"><p>乘法</p>
<p>整数除法</p>
<p>取模 (余数) </p></td>
</tr>
<tr class="even">
<td align="left"><p>+</p>
<p>-</p></td>
<td align="left"><p>加法</p>
<p>减法</p></td>
</tr>
<tr class="odd">
<td align="left"><p>&lt;&lt;</p>
<p>&gt;&gt;</p>
<p>&gt;&gt;&gt;</p></td>
<td align="left"><p>左移</p>
<p>逻辑右移位</p>
<p>算术右移位</p></td>
</tr>
<tr class="even">
<td align="left"><p>= (或 = =) </p>
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
<td align="left"><p><strong>和</strong> (或 &) </p></td>
<td align="left"><p>位与</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>xor</strong> (或 ^) </p></td>
<td align="left"><p>按位 XOR (异或) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>或</strong> (或 |) </p></td>
<td align="left"><p>按位“或”</p></td>
</tr>
</tbody>
</table>


如果表达式为 true，则 &lt; 、 &gt; 、=、= = 和！ = 比较运算符的计算结果为 1; 如果表达式为 false，则计算结果为零。 单个等号 (=) 与双等号 (= =) 相同。 不能在 MASM 表达式中使用副作用或赋值。

无效操作 (例如除以零) 导致 "操作数错误" 返回到 [调试器命令窗口](debugger-command-window.md)中。

## <a name="non-numeric-operators-in-masm-expressions"></a>MASM 表达式中的非数字运算符

还可以在 MASM 表达式中使用以下附加运算符。

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
<td align="left"><p><strong>$fnsucc (</strong> <em>FnAddress</em>， <em>RetVal</em>，<em>标志</em><strong>) </strong></p></td>
<td align="left"><p>将 <em>RetVal</em> 值解释为位于 <em>FnAddress</em> 地址的函数的返回值。 如果此返回值限定为成功代码， <strong>$fnsucc</strong> 将返回 <strong>TRUE</strong>。 否则， <strong>$fnsucc</strong> 返回 <strong>FALSE</strong>。</p>
<p>如果返回类型为 BOOL、bool、HANDLE、HRESULT 或 NTSTATUS， <strong>$fnsucc</strong> 会正确了解指定的返回值是否限定为成功代码。 如果返回类型是一个指针，则除 <strong>NULL</strong> 之外的所有值都将符合成功代码。 对于任何其他类型，success 都是通过 " <em>标志</em>" 的值来定义的。 如果 <em>标志</em> 为0，则非零值 <em>RetVal</em> 为 success。 如果 <em>标志</em> 为1，则值为0的 <em>RetVal</em> 为 success。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$iment (</strong><em>地址</em><strong>) </strong></p></td>
<td align="left"><p>返回已加载的模块列表中的图像入口点地址。 <em>Address</em> 指定 (PE) 映像基址的可移植可执行文件。 可通过在 <em>地址</em> 指定的图像的 PE 映像标头中查找图像入口点来找到条目。</p>
<p>可以将此函数用于模块列表中已存在的两个模块，并使用<strong><a href="bp--bu--bm--set-breakpoint-.md" data-raw-source="[bu](bp--bu--bm--set-breakpoint-.md)">bu</a></strong>命令设置<a href="unresolved-breakpoints---bu-breakpoints-.md" data-raw-source="[unresolved breakpoints](unresolved-breakpoints---bu-breakpoints-.md)">未解析的断点</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scmp ( "</strong><em>string1</em><strong>" 和 "</strong><em>string2</em><strong>" ) </strong></p></td>
<td align="left"><p>计算结果为-1、0或1，如 <strong>strcmp</strong> C 函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$sicmp ( "</strong><em>string1</em><strong>" 和 "</strong><em>string2</em><strong>" ) </strong></p></td>
<td align="left"><p>计算结果为-1、0或1，如 <strong>stricmp</strong> Microsoft Win32 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$spat ( "</strong><em>String</em><strong>"、"</strong><em>Pattern</em><strong>" ) </strong></p></td>
<td align="left"><p>计算结果为 <strong>TRUE</strong> 或 <strong>FALSE</strong> ，具体取决于 <em>字符串</em> 是否匹配 <em>模式</em>。 匹配不区分大小写。 <em>模式</em> 可以包含各种通配符和说明符。 有关语法的详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$vvalid (</strong><em>地址</em><strong>、</strong> <em>长度</em><strong>) </strong></p></td>
<td align="left"><p>确定从 <em>Address</em> 开始并为 <em>长度</em> 字节扩展的内存范围是否有效。 如果内存有效， <strong>$vvalid</strong> 的计算结果为1。 如果内存无效， <strong>$vvalid</strong> 的计算结果为0。</p></td>
</tr>
</tbody>
</table>

## <a name="registers-and-pseudo-registers-in-masm-expressions"></a>在 MASM 表达式中注册和 Pseudo-Registers

可以在 MASM 表达式中使用寄存器和伪寄存器。 你可以在 "所有寄存器" 和 "伪注册" 之前添加 at 符号 ( @ ) 。 At 符号使调试器能够更快地访问该值。 基于 x86 的最常见寄存器不需要此 at 符号。 对于其他寄存器和伪寄存器，建议你添加 at 符号，但实际上并不是必需的。 如果在不太常用的寄存器上省略 at 符号，则调试器会尝试将文本解析为十六进制数，然后将其作为符号，最后作为寄存器进行分析。

你还可以使用句点 (. ) 指示当前指令指针。 不应在此时间段之前添加 at 符号，也不能将句点用作 [**r 命令**](r--registers-.md)的第一个参数。 此时间段与 **$ip** 伪寄存器具有相同的含义。

有关寄存器和伪寄存器的详细信息，请参阅 [注册语法](register-syntax.md) 和 [伪寄存器语法](pseudo-register-syntax.md)。

## <a name="source-line-numbers-in-masm-expressions"></a>MASM 表达式中的源行号

您可以使用 MASM 表达式中的源文件和行号表达式。 必须使用抑音符 () 将这些表达式括起来 \` 。 有关语法的详细信息，请参阅 [源行语法](source-line-syntax.md)。

## <a name="see-also"></a>另请参阅

[MASM 表达式与C++ 表达式](masm-expressions-vs--c---expressions.md)

[混合表达式示例](expression-examples.md)

[C++ 数字和运算符](c---numbers-and-operators.md)

[符号扩展](sign-extension.md) 