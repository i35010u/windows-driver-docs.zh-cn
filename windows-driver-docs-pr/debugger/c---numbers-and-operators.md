---
title: C++ 数字和运算符
description: C++ 数字和运算符
ms.assetid: e5d3ac7f-fd79-48bb-b927-9ad72570dcbe
keywords:
- 表达式， C++表达式语法
- C++表达式，数值
- C++表达式，运算符
- 数值表达式，C++
- 运算符C++
- 优先规则（C++）
- 方法
- 方法、语法
- 类的成员
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01c862f6f1d0d3b49c5286ea47a7a4356ca40bd8
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910391"
---
# <a name="c-numbers-and-operators"></a>C++ 数字和运算符


## <span id="ddk_c_numbers_and_operators_dbg"></span><span id="DDK_C_NUMBERS_AND_OPERATORS_DBG"></span>


C++表达式分析器支持所有形式的C++表达式语法。 语法包括所有数据类型（包括指针、浮点数和数组）以及所有C++一元和二元运算符。

### <a name="span-idnumbers_in_c___expressionsspanspan-idnumbers_in_c___expressionsspannumbers-in-c-expressions"></a><span id="numbers_in_c___expressions"></span><span id="NUMBERS_IN_C___EXPRESSIONS"></span>表达式中C++的数字

表达式中C++的数字被解释为十进制数，除非以其他方式指定它们。 若要指定十六进制整数，请在数字前面加上**0x** 。 若要指定八进制整数，请在数字前面加上**0** （零）。

默认调试器基数不影响输入C++表达式的方式。 不能直接输入二进制数（除非在C++表达式内嵌套了 MASM 表达式）。

可以采用<em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em> **\`** <em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>格式输入十六进制64位值。 （还可以省略抑音符（ **\`** ）。）这两种格式都生成相同的值。

可以将**L**、 **U**和**I64**后缀与整数值一起使用。 所创建的数字的实际大小取决于后缀和输入的数字。 有关此解释的详细信息，请参阅C++语言参考。

表达式计算器的C++ *输出*保留表达式规则指定的数据类型。 C++ 但是，如果将此表达式用作命令的参数，将始终进行强制转换。 例如，当将整数值用作命令参数中的地址时，无需将其转换为指针。 如果无法将表达式的值有效地强制转换为整数或指针，则会出现语法错误。

可以为某些输出使用**0n** （十进制）前缀，但不能将其用于C++表达式输入。

### <a name="span-idcharacters_and_strings_in_c___expressionsspanspan-idcharacters_and_strings_in_c___expressionsspancharacters-and-strings-in-c-expressions"></a><span id="characters_and_strings_in_c___expressions"></span><span id="CHARACTERS_AND_STRINGS_IN_C___EXPRESSIONS"></span>表达式中的C++字符和字符串

可以通过使用单引号（'）将该字符括起来来输入。 允许使用C++标准转义符。

可以通过用双引号（"）将字符串括起来来输入字符串。 您可以使用 **\\"** 作为此类字符串中的转义序列。 但是，字符串对于[表达式计算器](evaluating-expressions.md)没有意义。

### <a name="span-idsymbols_in_c___expressionsspanspan-idsymbols_in_c___expressionsspansymbols-in-c-expressions"></a><span id="symbols_in_c___expressions"></span><span id="SYMBOLS_IN_C___EXPRESSIONS"></span>表达式中C++的符号

在C++表达式中，每个符号根据其类型进行解释。 根据符号的引用，可能会将其解释为整数、数据结构、函数指针或任何其他数据类型。 如果使用的符号不与C++ C++表达式中的数据类型（如未修改的模块名称）对应，则会出现语法错误。

如果符号可能不明确，可以添加模块名称和感叹号（ **！** ）或符号前面的感叹号。 有关符号识别的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

仅当在符号名称前面添加了模块名称和感叹号时，才可以在符号名称中使用抑音符（ **\`** ）或撇号（ **'** ）。

在模板名称后添加 **&lt;** 和 **&gt;** 分隔符后，可以在这些分隔符之间添加空格。

### <a name="span-idoperators_in_c___expressionsspanspan-idoperators_in_c___expressionsspanoperators-in-c-expressions"></a><span id="operators_in_c___expressions"></span><span id="OPERATORS_IN_C___EXPRESSIONS"></span>表达式中C++的运算符

始终可以使用括号覆盖优先规则。

如果将C++表达式的一部分括在括号中，并在表达式之前添加两个 at 符号（ **@@** ），则根据 MASM 表达式规则解释该表达式。 不能在两个 at 符号和左括号之间添加空格。 此表达式的最终值作为 ULONG64 值传递到C++表达式计算器。 还可以通过使用 **@@c+ + （...）** 或 **@@masm（...）** 来指定表达式计算器。

数据类型在C++语言中以常规方式指示。 指示数组（ **\[ \]** ）、指针成员（ **-&gt;** ）、UDT 成员（）的符号 **。** ）和类（ **：：** ）的成员都被识别。 支持所有算术运算符，包括赋值运算符和副作用运算符。 但是，不能使用**new**、 **delete**和**throw**运算符，也不能实际调用函数。

支持指针算法，并正确缩放偏移量。 请注意，不能添加函数指针的偏移量。 （如果必须将偏移量添加到函数指针，请先将偏移量强制转换为字符指针。）

与在C++中一样，如果使用的运算符的数据类型无效，则会出现语法错误。 调试器的表达式C++分析器使用比大多数C++编译器更宽松的规则，但所有主要规则都是强制执行的。 例如，不能移动非整数值。

您可以使用下列运算符。 每个单元中的运算符优先于位于较低单元格中的运算符。 相同单元中的运算符具有相同的优先级，并且是从左向右分析的。 与一起C++，如果表达式的值已知，则表达式计算结束。 这一结尾使你能够有效地使用诸如 **？？ myPtr & & \*myPtr**的表达式。

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
<td align="left"><p><em>Class</em> <strong>：：</strong> <em>Member</em></p>
<p><em>Class</em> <strong>：： ~</strong><em>Member</em></p>
<p><strong>：：</strong> <em>Name</em></p></td>
<td align="left"><p>类的成员</p>
<p>类的成员（析构函数）</p>
<p>全局</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>结构</em> <strong>。</strong> <em>字段</em></p>
<p><em>指针</em> <strong>-&gt;</strong> <em>字段</em></p>
<p><em>名称</em> <strong>[</strong><em>integer</em><strong>]</strong></p>
<p><em>LValue</em> <strong>++</strong></p>
<p><em>LValue</em> <strong>--</strong></p>
<p><strong>dynamic_cast &lt;</strong><em>类型</em><strong>&gt;（</strong><em>值</em><strong>）</strong></p>
<p><strong>static_cast &lt;</strong><em>类型</em><strong>&gt;（</strong><em>值</em><strong>）</strong></p>
<p><strong>reinterpret_cast &lt;</strong><em>类型</em><strong>&gt;（</strong><em>值</em><strong>）</strong></p>
<p><strong>const_cast &lt;</strong><em>类型</em><strong>&gt;（</strong><em>值</em><strong>）</strong></p></td>
<td align="left"><p>结构中的字段</p>
<p>引用结构中的字段</p>
<p>数组下标</p>
<p>递增（计算后）</p>
<p>减量（计算后）</p>
<p>转换（始终执行）</p>
<p>转换（始终执行）</p>
<p>转换（始终执行）</p>
<p>转换（始终执行）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>（</strong><em>类型</em><strong>）</strong> <em>值</em></p>
<p><strong>sizeof</strong> <em>值</em></p>
<p><strong>sizeof （</strong> <em>类型</em> <strong>）</strong></p>
<p><strong>++</strong> <em>LValue</em></p>
<p><strong>--</strong> <em>LValue</em></p>
<p><strong>~</strong> <em>值</em></p>
<p><strong>!</strong> <em>值</em></p>
<p><em>值</em></p>
<p><strong>+</strong><em>值</em></p>
<p><strong>&</strong> <em>LValue</em></p>
<p><strong><em></strong><em>值</em></p></td>
<td align="left"><p>转换（始终执行）</p>
<p>表达式的大小</p>
<p>数据类型的大小</p>
<p>递增（计算之前）</p>
<p>减量（计算之前）</p>
<p>位补数</p>
<p>Not （布尔值）</p>
<p>一元负</p>
<p>一元加</p>
<p>数据类型的地址</p>
<p>取消引用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>结构</em><strong>。 <em></strong><em>指针</em></p>
<p><em>指针</em> <strong>-&gt; *</strong> <em>指针</em></p></td>
<td align="left"><p>指向结构成员的指针</p>
<p>指向引用结构的成员的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p></em></strong><em>值</em><strong><em>值</em></p>
<p><em>值</em> <strong>/</strong> <em>值</em></p>
<p><em>值</em> <strong>%</strong> <em>值</em></p></td>
<td align="left"><p>倍增</p>
<p>部门</p>
<p>模块</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>+</strong> <em>值</em></p>
<p><em>值</em> <strong>-</strong> <em>值</em></p></td>
<td align="left"><p>相加</p>
<p>减法</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>&lt;</strong> <em>值</em>&lt;值</p>
<p><strong>&gt;</strong> <em>值</em>&gt;值</p></td>
<td align="left"><p>按位左移</p>
<p>按位右移</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>&lt;</strong> <em>值</em></p>
<p><strong>=</strong> <em>值</em>&lt;值</p>
<p><em>值</em> <strong>&gt;</strong> <em>值</em></p>
<p><strong>=</strong> <em>值</em>&gt;值</p></td>
<td align="left"><p>小于（比较）</p>
<p>小于或等于（比较）</p>
<p>大于（比较）</p>
<p>大于或等于（比较）</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>==</strong> <em>值</em></p>
<p><em>值</em> <strong>！ =</strong> <em>值</em></p></td>
<td align="left"><p>等于（比较）</p>
<p>不等于（比较）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>&</strong> <em>值</em></p></td>
<td align="left"><p>位与</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>^</strong> <em>值</em></p></td>
<td align="left"><p>按位 XOR （异或）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>|</strong> <em>值</em></p></td>
<td align="left"><p>按位“或”</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>&&</strong> <em>值</em></p></td>
<td align="left"><p>逻辑“与”</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>||</strong> <em>值</em></p></td>
<td align="left"><p>逻辑“或”</p></td>
</tr>
<tr class="even">
<td align="left">
<p><em>LValue</em> <strong>=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>*=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>/=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>%=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>+=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>-=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>&lt;&lt;=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>&gt;&gt;=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>&=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>|=</strong> <em>值</em></p>
<p><em>LValue</em> <strong>^=</strong> <em>值</em></p></td>
<td align="left"><p>分配</p>
<p>乘和赋值</p>
<p>除和赋值</p>
<p>取模并赋值</p>
<p>添加并分配</p>
<p>减并赋值</p>
<p>左移并分配</p>
<p>右移并分配</p>
<p>和分配</p>
<p>或并分配</p>
<p>XOR 和 assign</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>？</strong> <em>值</em> <strong>：</strong> <em>值</em></p></td>
<td align="left"><p>条件计算</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>、</strong> <em>值</em></p></td>
<td align="left"><p>计算所有值，然后放弃除最右边值之外的所有值</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idregisters_and_pseudo_registers_in_c___expressionsspanspan-idregisters_and_pseudo_registers_in_c___expressionsspanregisters-and-pseudo-registers-in-c-expressions"></a><span id="registers_and_pseudo_registers_in_c___expressions"></span><span id="REGISTERS_AND_PSEUDO_REGISTERS_IN_C___EXPRESSIONS"></span>表达式中C++的寄存器和伪寄存器

可以在表达式中C++使用寄存器和伪寄存器。 必须在注册或伪寄存器之前添加 at 符号（ **@** ）。

表达式计算器会自动执行正确的强制转换。 实际寄存器和整数值伪寄存器将强制转换为 ULONG64。 所有地址都将强制转换为 PUCHAR， **$thread**强制转换为 ETHREAD\*， **$PROC**转换为 EPROCESS\*， **$teb**强制转换为 teb\*， **$peb**强制转换为 peb\*。

不能通过赋值或副作用运算符来更改寄存器或伪寄存器。 必须使用[**r （寄存器）** ](r--registers-.md)命令更改这些值。

有关寄存器和伪寄存器的详细信息，请参阅[注册语法](register-syntax.md)和[伪寄存器语法](pseudo-register-syntax.md)。

### <a name="span-idmacros_in_c___expressionsspanspan-idmacros_in_c___expressionsspanmacros-in-c-expressions"></a><span id="macros_in_c___expressions"></span><span id="MACROS_IN_C___EXPRESSIONS"></span>表达式中C++的宏

可以在表达式中C++使用宏。 必须在宏前面添加数字符号（\#）。

您可以使用以下宏。 这些宏与具有相同名称的 Microsoft Windows 宏具有相同的定义。 （Windows 宏在 Winnt 中定义。）

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
<td align="left"><p>#CONTAINING_RECORD （<em>地址</em>、<em>类型</em>、<em>字段</em>）</p></td>
<td align="left"><p>如果给定结构的类型和结构内字段的地址，则返回结构实例的基址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#FIELD_OFFSET （<em>类型</em>、<em>字段</em>）</p></td>
<td align="left"><p>返回已知结构类型中命名字段的字节偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_CONTAINS_FIELD （<em>结构</em>、<em>大小</em>、<em>字段</em>）</p></td>
<td align="left"><p>指示给定的字节大小是否包含所需的字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_FIELD_SIZE （<em>类型</em>、<em>字段</em>）</p></td>
<td align="left"><p>返回已知类型的结构中字段的大小，而不需要字段的类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_NUMBER_OF （<em>Array</em>）</p></td>
<td align="left"><p>返回静态大小的数组中的元素数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_SIZEOF_THROUGH_FIELD （<em>类型</em>、<em>字段</em>）</p></td>
<td align="left"><p>返回已知类型的结构的大小，向上直到并包括指定的字段。</p></td>
</tr>
</tbody>
</table>

 

 

 





