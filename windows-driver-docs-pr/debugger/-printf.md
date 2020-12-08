---
title: .printf
description: Printf 标记的行为类似于 C 中的 printf 语句。
keywords:
- printf Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .printf
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c6cda709944a0da7bb62e7296b1b03d1dfed434
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795231"
---
# <a name="printf"></a>.printf


**Printf** 标记的行为类似于 C 中的 **printf** 语句。

```dbgcmd
.printf [/D] [Option] "FormatString" [, Argument , ...] 
```

## <a name="span-idsyntax_elementsspanspan-idsyntax_elementsspanspan-idsyntax_elementsspansyntax-elements"></a><span id="Syntax_Elements"></span><span id="syntax_elements"></span><span id="SYNTAX_ELEMENTS"></span>语法元素


<span id="_D"></span><span id="_d"></span>**/D**  
指定格式字符串包含 [调试器标记语言](debugger-markup-language-commands.md) (DML) 。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*选项*   
 (WinDbg 仅) 指定 WinDbg 应将格式说明符解释为的文本消息类型。 WinDbg 为每种类型的调试器指定命令窗口消息的背景和文本颜色;选择这些选项之一会使消息以适当的颜色显示。 默认情况下，将文本显示为普通级别的消息。 有关消息颜色以及如何设置它们的详细信息，请参阅 [View |选项](view---options.md)。

可以使用以下选项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">消息类型</th>
<th align="left">"选项" 对话框中的颜色标题</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>/od</p></td>
<td align="left"><p>对象</p></td>
<td align="left"><p>调试对象级别命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/oD</p></td>
<td align="left"><p>调试对象提示</p></td>
<td align="left"><p>调试对象提示级别命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/oe</p></td>
<td align="left"><p>error</p></td>
<td align="left"><p>错误级别命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/on</p></td>
<td align="left"><p>一般</p></td>
<td align="left"><p>普通级别命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/op</p></td>
<td align="left"><p>prompt</p></td>
<td align="left"><p>提示符级别命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/oP</p></td>
<td align="left"><p>提示寄存器</p></td>
<td align="left"><p>提示寄存器级别命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/os</p></td>
<td align="left"><p>symbols</p></td>
<td align="left"><p>符号消息级别命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ov</p></td>
<td align="left"><p>verbose</p></td>
<td align="left"><p>详细级别命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/ow</p></td>
<td align="left"><p>warning</p></td>
<td align="left"><p>警告级别命令窗口</p></td>
</tr>
</tbody>
</table>

 

<span id="_______FormatString______"></span><span id="_______formatstring______"></span><span id="_______FORMATSTRING______"></span>*格式字符串*   
指定格式字符串，如 **printf** 中所示。 通常，转换字符的工作方式与 C 中的完全一样。对于浮点转换字符，64位参数被解释为32位浮点数，除非使用 **l** 修饰符。

可以添加 "I64" 修饰符，以指示应将值解释为64位。 例如，可以使用 "% I64x" 来打印64位十六进制数字。

支持% p 转换字符，但它表示目标的虚拟地址空间中的指针。 它不能包含任何修饰符，它使用调试器的内部地址格式。 除了标准 printf 样式的格式说明符以外，还支持以下附加转换字符。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字符</th>
<th align="left">参数类型</th>
<th align="left">参数</th>
<th align="left">已打印文本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>% p</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的指针。</p></td>
<td align="left"><p>指针的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>% N</p></td>
<td align="left"><p>根据主机的体系结构，DWORD_PTR (32 或64位) </p></td>
<td align="left"><p>主机的虚拟地址空间中的指针。</p></td>
<td align="left"><p>指针的值。  (这等效于标准 C% p 字符。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>% ma</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中以 NULL 结尾的 ASCII 字符串的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>% mu</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中以 NULL 结尾的 Unicode 字符串的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>% msa</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中 ANSI_STRING 结构的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>% msu</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中 UNICODE_STRING 结构的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>% y</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中调试器符号的地址。</p></td>
<td align="left"><p>如果任何) ，则为包含指定符号 (和置换的名称的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>% ly</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中调试器符号的地址。</p></td>
<td align="left"><p>一个字符串，包含指定符号 (和置换的名称（如果) 有）以及任何可用的源行信息。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Arguments______"></span><span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span>*参数*   
指定格式字符串的参数，如 **printf** 中所示。 指定的参数数目应与 *格式说明符* 中的转换字符数相匹配。 每个自变量都是一个表达式，该表达式将由默认表达式计算器 (MASM 或 c + +) 进行计算。 有关详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

默认情况下，可以使用 *Options* 参数选择的颜色设置在白色背景上设置为黑色文本。 若要充分利用这些选项，必须先使用 [View |](view---options.md) 用于打开 "选项" 对话框的选项，并更改调试器的颜色设置命令窗口消息。

下面的示例演示如何在格式字符串中包含 DML 标记。

```dbgcmd
.printf /D "Click <link cmd=\".chain /D\">here</link> to see extensions DLLs."
```

![命令浏览器窗口中 dml 链接的屏幕截图](images/printf01.png)

上图中显示的输出包含一个链接，您可以单击该链接来执行标记中指定的命令 `<link>` 。 下图显示了单击链接的结果。

![命令浏览器窗口中 dml 输出的屏幕截图](images/printf02.png)

有关 DML 标记的信息，请参阅适用于 Windows 调试工具的安装文件夹中的 dml.doc。

 

 





