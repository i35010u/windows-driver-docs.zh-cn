---
title: C++ 数字和运算符
description: C++ 数字和运算符
ms.assetid: e5d3ac7f-fd79-48bb-b927-9ad72570dcbe
keywords:
- 表达式中，C++表达式语法
- C++表达式中数字
- C++表达式运算符
- 数值表达式，C++
- 运算符C++
- 优先顺序规则 (C++)
- 方法
- 方法语法
- 类的成员
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b294b37ad5627b6d7b708552a6da79e89cd6b1c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373960"
---
# <a name="c-numbers-and-operators"></a>C++ 数字和运算符


## <span id="ddk_c_numbers_and_operators_dbg"></span><span id="DDK_C_NUMBERS_AND_OPERATORS_DBG"></span>


C++的表达式分析器支持所有形式的C++表达式语法。 语法包括所有数据类型 （包括指针、 浮点数和数组） 和所有C++一元和二元运算符。

### <a name="span-idnumbersincexpressionsspanspan-idnumbersincexpressionsspannumbers-in-c-expressions"></a><span id="numbers_in_c___expressions"></span><span id="NUMBERS_IN_C___EXPRESSIONS"></span>统计中的C++表达式

统计中的C++表达式被解释为十进制数字，除非指定另一个的方式。 若要指定十六进制整数，添加**0x**数字前。 若要指定八进制整数，添加**0**数之前 （零）。

默认调试器基数不会影响如何输入C++表达式。 不能直接输入一个二进制数字 (除非通过嵌套中的 MASM 表达式C++表达式)。

可以输入中的十六进制 64 位值<em>xxxxxxxx</em>**\`**<em>xxxxxxxx</em>格式。 (您也可以省略重读符号 ( **\`** )。)这两种格式产生相同的值。

可以使用**L**， **U**，并**I64**的整数值的后缀。 创建数量的实际大小依赖于后缀和您输入的数字。 有关此解释的详细信息，请参阅C++语言参考。

*输出*的C++表达式计算器保留的数据类型C++表达式规则指定。 但是，如果您使用此表达式作为命令参数，是始终进行强制转换。 例如，无需使用作为命令参数中的地址时强制转换为指针的整数值。 如果表达式的值不能有效地转换为整数或指针，将发生语法错误。

可以使用**0n**某些 （十进制） 前缀*输出*，但你不能将其用于C++表达式输入。

### <a name="span-idcharactersandstringsincexpressionsspanspan-idcharactersandstringsincexpressionsspancharacters-and-strings-in-c-expressions"></a><span id="characters_and_strings_in_c___expressions"></span><span id="CHARACTERS_AND_STRINGS_IN_C___EXPRESSIONS"></span>字符和字符串在C++表达式

可以通过用单引号 （'） 括起该输入字符。 标准C++允许使用转义字符。

可以通过使用双引号引起来 （'） 包围它们输入字符串文本。 可以使用 **\\"** 作为此类字符串内转义序列。 但是，字符串必须无意义[表达式计算器](evaluating-expressions.md)。

### <a name="span-idsymbolsincexpressionsspanspan-idsymbolsincexpressionsspansymbols-in-c-expressions"></a><span id="symbols_in_c___expressions"></span><span id="SYMBOLS_IN_C___EXPRESSIONS"></span>在符号C++表达式

在C++表达式，每个符号解释根据其类型。 具体取决于符号所引用的内容，可能会被解释为整数、 数据结构、 函数指针或任何其他数据类型。 如果使用不对应的符号C++数据类型 （例如未修改的模块名称） 中C++表达式中，发生语法错误。

如果该符号可能是不明确，则可以添加的模块名称和一个感叹号 ( **！** ) 或仅有一个感叹号符号之前。 有关符号识别的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

可以使用的重读符号 ( **\`** ) 或撇号 (  ) 中的符号名称只有在添加的模块名称和感叹号符号名称前。

当您将添加**&lt;** 并**&gt;** 分隔符后的模板名称，您可以添加这些分隔符之间的空格。

### <a name="span-idoperatorsincexpressionsspanspan-idoperatorsincexpressionsspanoperators-in-c-expressions"></a><span id="operators_in_c___expressions"></span><span id="OPERATORS_IN_C___EXPRESSIONS"></span>中的运算符C++表达式

您始终可以使用括号替代优先顺序规则。

如果您用括起来的一部分C++在括号中的表达式，并添加两个 at 符号 (**@@**) 先于表达式，该表达式将解释根据 MASM 表达式规则。 无法添加这两个 at 符号和左括号之间有空格。 此表达式的最终值传递给C++作为 ULONG64 值的表达式计算器。 此外可以通过使用指定表达式计算器 **@@c+ + （...）** 或 **@@masm（...）**.

像往常一样在指示数据类型C++语言。 指示数组的符号 ( **\[ \]** )，指针成员 ( **- &gt;** )，UDT 成员 ( **。** )，和类的成员 ( **::** ) 所有识别。 支持的所有算术运算符，包括赋值和副作用的运算符。 但是，不能使用**新**，**删除**，并**引发**运算符，并且您不能实际调用的函数。

支持指针算法和偏移量进行正确缩放。 请注意，不能将某一偏移量添加到函数指针。 （如果您必须将某一偏移量添加到函数指针，强制转换到字符指针的偏移量第一次。）

在C++，如果您使用运算符具有无效的数据类型发生语法错误。 调试器的C++的表达式分析器使用比大多数稍微更宽松的规则C++编译器，但所有主要规则强制执行。 例如，不能将非整数值。

可以使用以下运算符。 每个单元格中的运算符优先于较小的单元中。 相同单元中的运算符均属于相同的优先级，从左到右进行分析。 与C++，表达式计算结束时才知道其值。 此结束，可有效地使用如下所示的表达式 **?? myPtr & & \*myPtr**。

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
<td align="left"><p><em>表达式</em> <strong>//</strong> <em>注释</em></p></td>
<td align="left"><p>忽略所有后续文本</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>类</em> <strong>::</strong><em>成员</em></p>
<p><em>类</em> <strong>:: ~</strong><em>成员</em></p>
<p><strong>::</strong><em>名称</em></p></td>
<td align="left"><p>类的成员</p>
<p>类 （析构函数） 的成员</p>
<p>全局</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>结构</em> <strong>。</strong> <em>字段</em></p>
<p><em>指针</em> <strong>- &gt;</strong> <em>字段</em></p>
<p><em>Name</em> <strong>[</strong><em>integer</em><strong>]</strong></p>
<p><em>LValue</em> <strong>++</strong></p>
<p><em>LValue</em> <strong>--</strong></p>
<p><strong>dynamic_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p>
<p><strong>static_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p>
<p><strong>reinterpret_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p>
<p><strong>const_cast &lt;</strong><em>type</em><strong>&gt;(</strong><em>Value</em><strong>)</strong></p></td>
<td align="left"><p>结构中的字段</p>
<p>引用结构中的字段</p>
<p>数组下标</p>
<p>增量 （之后评估版）</p>
<p>递减 （后评估版）</p>
<p>类型转换 （始终执行）</p>
<p>类型转换 （始终执行）</p>
<p>类型转换 （始终执行）</p>
<p>类型转换 （始终执行）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>(</strong><em>type</em><strong>)</strong> <em>Value</em></p>
<p><strong>sizeof</strong> <em>value</em></p>
<p><strong>sizeof(</strong> <em>type</em> <strong>)</strong></p>
<p><strong>++</strong> <em>左值</em></p>
<p><strong>--</strong> <em>左值</em></p>
<p><strong>~</strong> <em>值</em></p>
<p><strong>\!</strong> <em>值</em></p>
<p><em>值</em></p>
<p><strong>+</strong> <em>值</em></p>
<p><strong>&amp;</strong> <em>左值</em></p>
<p><strong><em></strong> <em>值</em></p></td>
<td align="left"><p>类型转换 （始终执行）</p>
<p>表达式的大小</p>
<p>数据类型的大小</p>
<p>增量 （之前评估版）</p>
<p>递减 （在之前评估版）</p>
<p>位求补</p>
<p>不 （布尔值）</p>
<p>一元负</p>
<p>一元加</p>
<p>数据类型的地址</p>
<p>取消引用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>结构</em> <strong>。 <em></strong> <em>指针</em></p>
<p><em>Pointer</em> <strong>-&gt; *</strong> <em>Pointer</em></p></td>
<td align="left"><p>指向成员的结构的指针</p>
<p>指向引用结构成员的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong></em></strong> <em>Value</em></p>
<p><em>Value</em> <strong>/</strong> <em>Value</em></p>
<p><em>Value</em> <strong>%</strong> <em>Value</em></p></td>
<td align="left"><p>乘法</p>
<p>部门</p>
<p>取模</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>+</strong> <em>Value</em></p>
<p><em>Value</em> <strong>-</strong> <em>Value</em></p></td>
<td align="left"><p>添加</p>
<p>减法</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>&lt;&lt;</strong> <em>Value</em></p>
<p><em>Value</em> <strong>&gt;&gt;</strong> <em>Value</em></p></td>
<td align="left"><p>按位左移</p>
<p>按位右移</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>&lt;</strong> <em>Value</em></p>
<p><em>Value</em> <strong>&lt;=</strong> <em>Value</em></p>
<p><em>Value</em> <strong>&gt;</strong> <em>Value</em></p>
<p><em>Value</em> <strong>&gt;=</strong> <em>Value</em></p></td>
<td align="left"><p>早于 （比较）</p>
<p>小于或等于 （比较）</p>
<p>大于 （比较）</p>
<p>大于或等于 （比较）</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>==</strong> <em>Value</em></p>
<p><em>Value</em> <strong>!=</strong> <em>Value</em></p></td>
<td align="left"><p>等于 （比较）</p>
<p>不等于 （比较）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>&amp;</strong> <em>Value</em></p></td>
<td align="left"><p>位与</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>^</strong> <em>Value</em></p></td>
<td align="left"><p>按位 XOR （异或）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>|</strong> <em>Value</em></p></td>
<td align="left"><p>按位 OR 运算符</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Value</em> <strong>&amp;&amp;</strong> <em>Value</em></p></td>
<td align="left"><p>逻辑与</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Value</em> <strong>||</strong> <em>Value</em></p></td>
<td align="left"><p>逻辑或</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>LValue</em> <strong>=</strong><em>Value</em></p>
<p><em>LValue</em> <strong></em>=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>/=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>%=</strong><em>Value</em></p>
<p><em>LValue</em> <strong>+=</strong><em>Value</em></p>
<p><em>LValue</em> <strong>-=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>&lt;&lt;=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>&gt;&gt;=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>&amp;=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>|=</strong> <em>Value</em></p>
<p><em>LValue</em> <strong>^=</strong> <em>Value</em></p></td>
<td align="left"><p>分配</p>
<p>乘并赋值</p>
<p>相除并赋值</p>
<p>取模和分配</p>
<p>添加和分配</p>
<p>相减并赋值</p>
<p>左移位，并将分配</p>
<p>右移位和分配</p>
<p>和分配</p>
<p>或和分配</p>
<p>XOR 并赋值</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>？</strong> <em>值</em> <strong>:</strong><em>值</em></p></td>
<td align="left"><p>条件评估</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>，</strong> <em>值</em></p></td>
<td align="left"><p>评估所有值，然后丢弃最右侧的值之外的所有</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idregistersandpseudoregistersincexpressionsspanspan-idregistersandpseudoregistersincexpressionsspanregisters-and-pseudo-registers-in-c-expressions"></a><span id="registers_and_pseudo_registers_in_c___expressions"></span><span id="REGISTERS_AND_PSEUDO_REGISTERS_IN_C___EXPRESSIONS"></span>寄存器和伪寄存器中的C++表达式

寄存器和伪寄存器中的可以使用C++表达式。 必须添加 at 符号 ( **@** ) 之前注册或伪寄存器。

表达式计算器会自动执行正确的强制转换。 实际的寄存器和整数值伪寄存器是强制转换为 ULONG64。 所有地址都转换为 PUCHAR， **$thread**强制都转换为 ETHREAD\*， **$proc**被强制都转换为 EPROCESS\*， **$teb**被强制都转换为 TEB\*，并 **$peb**被强制转换为 PEB\*。

不能更改注册或伪寄存器分配或副作用的运算符。 必须使用[ **r （寄存器）** ](r--registers-.md)命令来更改这些值。

有关寄存器和伪寄存器的详细信息，请参阅[注册语法](register-syntax.md)并[伪寄存器语法](pseudo-register-syntax.md)。

### <a name="span-idmacrosincexpressionsspanspan-idmacrosincexpressionsspanmacros-in-c-expressions"></a><span id="macros_in_c___expressions"></span><span id="MACROS_IN_C___EXPRESSIONS"></span>中的宏C++表达式

可以使用中的宏C++表达式。 必须添加数字符号 (\#) 之前的宏。

可以使用以下宏。 这些宏所具有的相同定义的具有相同名称的 Microsoft Windows 宏。 （Windows 宏的定义在 Winnt.h 中。）

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">返回值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>#CONTAINING_RECORD (<em>地址</em>，<em>类型</em>，<em>字段</em>)</p></td>
<td align="left"><p>返回给定类型的结构和结构中的字段的地址结构的实例的基址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#FIELD_OFFSET (<em>类型</em>，<em>字段</em>)</p></td>
<td align="left"><p>返回命名的字段的字节偏移量中的已知的结构类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_CONTAINS_FIELD (<em>Struct</em>，<em>大小</em>，<em>字段</em>)</p></td>
<td align="left"><p>指示给定的字节大小是否包括所需的字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_FIELD_SIZE(<em>Type</em>, <em>Field</em>)</p></td>
<td align="left"><p>而无需字段的类型返回已知类型的结构中的字段的大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_NUMBER_OF(<em>Array</em>)</p></td>
<td align="left"><p>以静态方式调整大小的数组中返回元素的数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_SIZEOF_THROUGH_FIELD(<em>Type</em>, <em>Field</em>)</p></td>
<td align="left"><p>通过和包括在指定的字段会返回已知类型的结构的大小。</p></td>
</tr>
</tbody>
</table>

 

 

 





