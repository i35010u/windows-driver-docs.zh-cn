---
title: C++ 数字和运算符
description: C++ 数字和运算符
keywords:
- 表达式，c + + 表达式语法
- C + + 表达式，数字
- C + + 表达式，运算符
- 数值表达式，c + +
- 运算符，c + +
- '优先规则 (c + +) '
- 方法
- 方法、语法
- 类的成员
ms.date: 03/31/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 6324e0cb9b197b6f3d9689a30f995631b937a131
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113626"
---
# <a name="c-numbers-and-operators"></a>C++ 数字和运算符

C + + 表达式分析器支持所有形式的 c + + 表达式语法。 语法包括所有数据类型 (包括指针、浮点数和数组) 以及所有 c + + 一元运算符和二元运算符。

调试器中的 "监视" 和 "局部变量" 窗口始终使用 c + + 表达式计算器。

在此示例中，" [？" ("计算 c + + 表达式") ](----evaluate-c---expression-.md) 命令显示指令指针寄存器的值。

```dbgcmd
0:000> ?? @eip
unsigned int 0x771e1a02
```

我们可以使用 c + + 运算符（例如 sizeof 函数）来确定结构的大小。

```dbgcmd
0:000> ?? (sizeof(_TEB))
unsigned int 0x1000
```

## <a name="set-the-expression-evaluator-to-c"></a>将表达式计算器设置为 c + +

使用 [. expr (选择表达式计算器) ](-expr--choose-expression-evaluator-.md) 以查看默认表达式计算器的定义，并将其更改为 c + +。

```dbgcmd
0:000> .expr
Current expression evaluator: MASM - Microsoft Assembler expressions
0:000> .expr /s c++
Current expression evaluator: C++ - C++ source expressions
```

由于已更改了默认表达式计算器，因此 " [ (计算表达式") ](---evaluate-expression-.md) 命令可用于显示 c + + 表达式。 此示例显示指令指针寄存器的值。 

```dbgcmd
0:000> ? @eip
Evaluate expression: 1998461442 = 771e1a02
```
Register @eip [语法](register-syntax.md)中更详细地介绍了的注册参考。

在此示例中，将0xD 的十六进制值添加到 eip 寄存器。

```dbgcmd
0:000> ? @eip + 0xD
Evaluate expression: 1998461455 = 771e1a0f
```

## <a name="registers-and-pseudo-registers-in-c-expressions"></a>C + + 表达式中的寄存器和 Pseudo-Registers

您可以在 c + + 表达式内使用寄存器和伪寄存器。 必须在 **@** 注册或伪寄存器之前添加 at 符号 ( ) 。

表达式计算器会自动执行正确的强制转换。 实际寄存器和整数值伪寄存器将强制转换为 ULONG64。 所有地址都将强制转换为 PUCHAR， **$thread** 强制转换为 ETHREAD \* ， **$proc** 转换为 EPROCESS \* ， **$teb** 转换为 TEB \* ，并将 **$peb** 强制转换为 peb \* 。


此示例显示 TEB。

```dbgcmd
0:000>  ?? @$teb
struct _TEB * 0x004ec000
   +0x000 NtTib            : _NT_TIB
   +0x01c EnvironmentPointer : (null) 
   +0x020 ClientId         : _CLIENT_ID
   +0x028 ActiveRpcHandle  : (null) 
   +0x02c ThreadLocalStoragePointer : 0x004ec02c Void
   +0x030 ProcessEnvironmentBlock : 0x004e9000 _PEB
   +0x034 LastErrorValue   : 0xbb
   +0x038 CountOfOwnedCriticalSections : 0
```

不能通过赋值或副作用运算符来更改寄存器或伪寄存器。 必须使用 [r (寄存器) ](r--registers-.md) 命令更改这些值。

此示例将伪寄存器设置为值5，然后将其显示。

```dbgcmd
0:000> r $t0 = 5

0:000> ?? @$t0
unsigned int64 5
```

有关寄存器和伪寄存器的详细信息，请参阅 [注册语法](register-syntax.md) 和 [伪寄存器语法](pseudo-register-syntax.md)。


## <a name="numbers-in-c-expressions"></a>C + + 表达式中的数字

C + + 表达式中的数字被解释为十进制数，除非以其他方式指定它们。 若要指定十六进制整数，请在数字前面加上 **0x** 。 若要指定八进制整数，请在数字前面加上 **0** (零) 。

默认调试器基数不影响输入 c + + 表达式的方式。 您不能直接输入 (的二进制数字，只是在 c + + 表达式) 中嵌套一个 MASM 表达式。

可以采用 <em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>格式输入十六进制64位值 **\`** <em></em> 。  (还可以省略 ) 的抑音符 ( **\`** 。 ) 两种格式都生成相同的值。

可以将 **L**、 **U** 和 **I64** 后缀与整数值一起使用。 所创建的数字的实际大小取决于后缀和输入的数字。 有关此解释的详细信息，请参阅 c + + 语言参考。

C + + 表达式计算器的 *输出* 保留 c + + 表达式规则指定的数据类型。 但是，如果将此表达式用作命令的参数，将始终进行强制转换。 例如，当将整数值用作命令参数中的地址时，无需将其转换为指针。 如果无法将表达式的值有效地强制转换为整数或指针，则会出现语法错误。

可以为某些 *输出* 使用 **0n** (decimal) 前缀，但不能将其用于 c + + 表达式输入。

## <a name="characters-and-strings-in-c-expressions"></a>C + + 表达式中的字符和字符串

您可以输入一个字符，用单引号将它括起来， ( ") 。 允许使用标准 c + + 转义字符。

您可以输入字符串，方法是使用双引号将它们括起来 ( ") 。 您可以使用 **\\ "** 作为此类字符串中的转义序列。 但是，字符串对于 [表达式计算器](evaluating-expressions.md)没有意义。

## <a name="symbols-in-c-expressions"></a>C + + 表达式中的符号

在 c + + 表达式中，每个符号根据其类型进行解释。 根据符号的引用，可能会将其解释为整数、数据结构、函数指针或任何其他数据类型。 如果使用的符号与 c + + 数据类型不对应 (例如 c + + 表达式中未修改的模块名称) ，则会出现语法错误。

如果符号可能不明确，可以 ( 中添加模块名称和感叹号 **！** 符号前面 ) 或仅一个惊叹号。 有关符号识别的详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

**\`** 仅当在符号名称前添加模块名称和感叹号时，才能在符号名称中使用抑音符 ( ) 或撇号 ( **"** ) 。

在 **&lt;** **&gt;** 模板名称后添加和分隔符后，可以在这些分隔符之间添加空格。

在 c + + 表达式中，将根据符号的类型解释每个符号。 根据符号的引用，可能会将其解释为整数、数据结构、函数指针或任何其他数据类型。 不对应于 c + + 数据类型的符号 (如未修改的模块名称) 创建语法错误。

如果符号可能不明确，请在其前面加上模块名称，将感叹号 (！ ). 如果符号名称可以解释为十六进制数，请在其前面加上模块名称，将感叹号 (！ ) 或仅惊叹号。 若要指定某个符号应为本地符号，请省略该模块名称，并将一个货币符号和一个惊叹号 ( $！ 符号名称前 ) 。 有关解释符号的详细信息，请参阅符号语法和符号匹配。

## <a name="structures-in-c-expressions"></a>C + + 表达式中的结构

C + + 表达式计算器将伪寄存器强制转换为相应的类型。 例如， **$teb** 将强制转换为 teb \* 。 

```dbgcmd
0:000> ??  @$teb
struct _TEB * 0x004ec000
   +0x000 NtTib            : _NT_TIB
   +0x01c EnvironmentPointer : (null) 
   +0x020 ClientId         : _CLIENT_ID
   +0x028 ActiveRpcHandle  : (null) 
   +0x02c ThreadLocalStoragePointer : 0x004ec02c Void
   +0x030 ProcessEnvironmentBlock : 0x004e9000 _PEB
   +0x034 LastErrorValue   : 0xbb
   +0x038 CountOfOwnedCriticalSections : 0
```

下面的示例显示了 TEB 结构中的进程 ID，该 ID 显示了指向所引用结构的成员的指针的使用。

```dbgcmd
0:000> ??  @$teb->ClientId.UniqueProcess
void * 0x0000059c
```

## <a name="operators-in-c-expressions"></a>C + + 表达式中的运算符

始终可以使用括号覆盖优先规则。

如果将 c + + 表达式的一部分括在括号中，并在表达式之前添加了两个 at 符号 (**@@**) ，则根据 MASM 表达式规则解释该表达式。 不能在两个 at 符号和左括号之间添加空格。 此表达式的最终值作为 ULONG64 值传递到 c + + 表达式计算器。 还可以通过使用 **@ @c + + ( ... )** 或 **@ @masm ( ... )** 来指定表达式计算器。

数据类型在 c + + 语言中以常规方式指示。 指示数组 ( **\[ \]** ) 、指针成员 ( **-&gt;** ) 、UDT 成员 ( 的符号 **。** ) 和 ( **：：** ) 类的成员都被识别。 支持所有算术运算符，包括赋值运算符和副作用运算符。 但是，不能使用 **new**、 **delete** 和 **throw** 运算符，也不能实际调用函数。

支持指针算法，并正确缩放偏移量。 请注意，不能添加函数指针的偏移量。  (如果必须添加对函数指针的偏移量，请先将偏移量强制转换为字符指针。 ) 

与在 c + + 中一样，如果使用的运算符的数据类型无效，则会出现语法错误。 调试器的 c + + 表达式分析器使用比大多数 c + + 编译器更宽松的规则，但会强制实施所有主要规则。 例如，不能移动非整数值。

您可以使用下列运算符。 每个单元中的运算符优先于位于较低单元格中的运算符。 相同单元中的运算符具有相同的优先级，并且是从左向右分析的。 

与 c + + 一样，表达式计算在其值已知时结束。 这一结尾使你可以有效地使用表达式，例如 **？？ myPtr && \* myPtr**。

### <a name="reference-and-type-casting"></a>引用和类型强制转换

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
<td align="left"><p><em>表达式</em> <strong>//</strong><em>注释</em></p></td>
<td align="left"><p>忽略所有后续文本</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Class</em> <strong>：：</strong> <em>Member</em></p>
<p><em>Class</em> <strong>：： ~</strong><em>Member</em></p>
<p><strong>：：</strong> <em>Name</em></p></td>
<td align="left"><p>类的成员</p>
<p>类的成员 (析构函数) </p>
<p>全球</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>结构</em> <strong>。</strong> <em>字段</em></p>
<p><em>指针</em> <strong>-&gt;</strong><em>字段</em></p>
<p><em>名称</em> <strong>[</strong><em>integer</em><strong>]</strong></p>
<p><em>LValue</em><strong>++</strong></p>
<p><em>LValue</em><strong>--</strong></p>
<p><strong>dynamic_cast &lt; </strong><em>键入</em><strong> &gt; (</strong><em>值</em><strong>) </strong></p>
<p><strong>static_cast &lt; </strong><em>键入</em><strong> &gt; (</strong><em>值</em><strong>) </strong></p>
<p><strong>reinterpret_cast &lt; </strong><em>键入</em><strong> &gt; (</strong><em>值</em><strong>) </strong></p>
<p><strong>const_cast &lt; </strong><em>键入</em><strong> &gt; (</strong><em>值</em><strong>) </strong></p></td>
<td align="left"><p>结构中的字段</p>
<p>引用结构中的字段</p>
<p>数组下标</p>
<p>计算后 (递增) </p>
<p>计算后递减 () </p>
<p>转换 (始终执行) </p>
<p>转换 (始终执行) </p>
<p>转换 (始终执行) </p>
<p>转换 (始终执行) </p></td>
</tr>
</tbody>
</table>

### <a name="value-operations"></a>值操作

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
<tr class="even">
<td align="left"><p><strong> (</strong><em>类型</em><strong>) </strong> <em>值</em></p>
<p><strong>sizeof</strong> <em>值</em></p>
<p><strong>sizeof (</strong> <em>类型</em> <strong>) </strong></p>
<p><strong>++</strong><em>LValue</em></p>
<p><strong>--</strong><em>LValue</em></p>
<p><strong>~</strong><em>值</em></p>
<p><strong>!</strong> <em>值</em></p>
<p><em>值</em></p>
<p><strong>+</strong> Value</p>
<p><strong>&</strong><em>LValue</em></p>
<p><strong><em></strong><em>值</em></p></td>
<td align="left"><p>转换 (始终执行) </p>
<p>表达式的大小</p>
<p>数据类型的大小</p>
<p>计算) 之前递增 (</p>
<p>计算) 之前递减 (</p>
<p>位补数</p>
<p>不 (布尔) </p>
<p>一元负</p>
<p>一元加</p>
<p>数据类型的地址</p>
<p>Dereference</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>结构</em> <strong> 。 <em></strong><em>指针</em></p>
<p><em>指针</em> <strong>-&gt; *</strong><em>指针</em></p></td>
<td align="left"><p>指向结构成员的指针</p>
<p>指向引用结构的成员的指针</p></td>
</tr>
</tbody>
</table>

### <a name="arithmetic"></a>算术

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
<tr class="even">
<td align="left"><p><em></em> <strong> 值 </em></strong><em>值</em></p>
<p><em>值</em> <strong>/</strong><em>值</em></p>
<p><em>值</em> <strong>%</strong><em>值</em></p></td>
<td align="left"><p>乘法</p>
<p>除法</p>
<p>Modulus</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>+</strong><em>值</em></p>
<p><em>值</em> <strong>-</strong><em>值</em></p></td>
<td align="left"><p>加法</p>
<p>减法</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>&lt;&lt;</strong><em>值</em></p>
<p><em>值</em> <strong>&gt;&gt;</strong><em>值</em></p></td>
<td align="left"><p>按位左移</p>
<p>按位右移</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>&lt;</strong><em>值</em></p>
<p><em>值</em> <strong>&lt;=</strong><em>值</em></p>
<p><em>值</em> <strong>&gt;</strong><em>值</em></p>
<p><em>值</em> <strong>&gt;=</strong><em>值</em></p></td>
<td align="left"><p>小于 (比较) </p>
<p>小于等于 (比较) </p>
<p>大于 (比较) </p>
<p>大于或等于 (比较) </p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>==</strong><em>值</em></p>
<p><em>值</em> <strong>！ =</strong> <em>值</em></p></td>
<td align="left"><p>相等 (比较) </p>
<p>不等于 (比较) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>&</strong><em>值</em></p></td>
<td align="left"><p>位与</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>^</strong><em>值</em></p></td>
<td align="left"><p>按位 XOR (异或) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>|</strong><em>值</em></p></td>
<td align="left"><p>按位“或”</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>&&</strong><em>值</em></p></td>
<td align="left"><p>逻辑与</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>值</em> <strong>||</strong><em>值</em></p></td>
<td align="left"><p>逻辑或</p></td>
</tr>
</tbody>
</table>

下面的示例假定将伪寄存器设置为 "已显示"。

```dbgcmd
0:000> r $t0 = 0
0:000> r $t1 = 1
0:000> r $t2 = 2
```

```dbgcmd
0:000> ?? @$t1 + @$t2
unsigned int64 3
0:000> ?? @$t2/@$t1
unsigned int64 2
0:000> ?? @$t2|@$t1
unsigned int64 3
```
### <a name="assignment"></a>分配

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
<tr class="even">
<td align="left">
<p><em>LValue</em> <strong>=</strong><em>值</em></p>
<p><em>LValue</em> <strong>*=</strong><em>值</em></p>
<p><em>LValue</em> <strong>/=</strong><em>值</em></p>
<p><em>LValue</em> <strong>%=</strong><em>值</em></p>
<p><em>LValue</em> <strong>+=</strong><em>值</em></p>
<p><em>LValue</em> <strong>-=</strong><em>值</em></p>
<p><em>LValue</em> <strong>&lt;&lt;=</strong><em>值</em></p>
<p><em>LValue</em> <strong>&gt;&gt;=</strong><em>值</em></p>
<p><em>LValue</em> <strong>&=</strong><em>值</em></p>
<p><em>LValue</em> <strong>|=</strong><em>值</em></p>
<p><em>LValue</em> <strong>^=</strong><em>值</em></p></td>
<td align="left"><p>赋值</p>
<p>乘并赋值</p>
<p>除并赋值</p>
<p>取模并赋值</p>
<p>添加并赋值</p>
<p>相减并赋值</p>
<p>左移并分配</p>
<p>右移并分配</p>
<p>和分配</p>
<p>或并分配</p>
<p>XOR 和 assign</p></td>
</tr>
</tbody>
</table>

### <a name="evaluation"></a>计算

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
<td align="left"><p><em>值</em> <strong>？</strong> <em>值</em> <strong>：</strong> <em>值</em></p></td>
<td align="left"><p>条件计算</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>值</em> <strong>、</strong> <em>值</em></p></td>
<td align="left"><p>计算所有值，然后放弃除最右边值之外的所有值</p></td>
</tr>
</tbody>
</table>


### <a name="macros-in-c-expressions"></a>C + + 表达式中的宏

您可以在 c + + 表达式内使用宏。 必须在宏前面添加数字符号 (\#) 。

您可以使用以下宏。 这些宏与具有相同名称的 Microsoft Windows 宏具有相同的定义。  (在 Winnt 中定义 Windows 宏。 ) 

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
<td align="left"><p>#CONTAINING_RECORD (<em>地址</em>、 <em>类型</em>、 <em>字段</em>) </p></td>
<td align="left"><p>如果给定结构的类型和结构内字段的地址，则返回结构实例的基址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#FIELD_OFFSET (<em>类型</em>， <em>字段</em>) </p></td>
<td align="left"><p>返回已知结构类型中命名字段的字节偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_CONTAINS_FIELD (<em>结构</em>、 <em>大小</em>、 <em>字段</em>) </p></td>
<td align="left"><p>指示给定的字节大小是否包含所需的字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_FIELD_SIZE (<em>类型</em>， <em>字段</em>) </p></td>
<td align="left"><p>返回已知类型的结构中字段的大小，而不需要字段的类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#RTL_NUMBER_OF (<em>数组</em>) </p></td>
<td align="left"><p>返回静态大小的数组中的元素数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>#RTL_SIZEOF_THROUGH_FIELD (<em>类型</em>， <em>字段</em>) </p></td>
<td align="left"><p>返回已知类型的结构的大小，向上直到并包括指定的字段。</p></td>
</tr>
</tbody>
</table>


此示例演示如何使用 #FIELD_OFFSET 宏来计算结构中字段的字节偏移量。

```dbgcmd
0:000> ?? #FIELD_OFFSET(_PEB, BeingDebugged)
long 0n2
```

## <a name="see-also"></a>另请参阅 

[MASM 表达式与C++ 表达式](masm-expressions-vs--c---expressions.md)
 
[?? (评估 c + + 表达式) ](----evaluate-c---expression-.md)

[? (计算表达式) ](---evaluate-expression-.md) 

[.expr（选择表达式评估器）](-expr--choose-expression-evaluator-.md)

[符号扩展](sign-extension.md) 

[混合表达式示例](expression-examples.md)
 




