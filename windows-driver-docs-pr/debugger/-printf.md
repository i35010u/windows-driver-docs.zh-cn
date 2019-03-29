---
title: .printf
description: .Printf 令牌的行为类似于在 C 中的 printf 语句
ms.assetid: 16ad25c4-7df3-490e-80da-2beaddec3230
keywords:
- .printf Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .printf
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04ab8f9d5a680c1b5118a2b051e64ed7d156a6ff
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350332"
---
# <a name="printf"></a>.printf


**.Printf**令牌的行为类似于**printf**在 C 中的语句

```dbgcmd
.printf [/D] [Option] "FormatString" [, Argument , ...] 
```

## <a name="span-idsyntaxelementsspanspan-idsyntaxelementsspanspan-idsyntaxelementsspansyntax-elements"></a><span id="Syntax_Elements"></span><span id="syntax_elements"></span><span id="SYNTAX_ELEMENTS"></span>语法元素


<span id="_D"></span><span id="_d"></span>**/D**  
指定的格式字符串包含[调试器标记语言](debugger-markup-language-commands.md)(DML)。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *选项*   
(仅 WinDbg)指定 WinDbg 应解释为格式字符串的短信的类型。 WinDbg 分配每个类型的调试器命令窗口消息背景和文本颜色;选择以下选项之一会导致在适当的颜色显示的消息。 默认值是将文本显示为正常级别消息。 消息颜色，以及如何将其设置的详细信息，请参阅[视图 |选项](view---options.md)。

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
<th align="left">选项对话框中的颜色的标题</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>/od</p></td>
<td align="left"><p>调试对象</p></td>
<td align="left"><p>调试对象级别的命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/oD</p></td>
<td align="left"><p>调试对象提示符</p></td>
<td align="left"><p>调试对象级别命令提示窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/oe</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>错误级别的命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/on</p></td>
<td align="left"><p>正常</p></td>
<td align="left"><p>标准级别的命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/op</p></td>
<td align="left"><p>prompt</p></td>
<td align="left"><p>级别命令提示窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/oP</p></td>
<td align="left"><p>提示符下注册</p></td>
<td align="left"><p>提示符下注册级别的命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/os</p></td>
<td align="left"><p>符号</p></td>
<td align="left"><p>符号消息级别的命令窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ov</p></td>
<td align="left"><p>详细</p></td>
<td align="left"><p>详细级别的命令窗口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/ow</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>警告级别的命令窗口</p></td>
</tr>
</tbody>
</table>

 

<span id="_______FormatString______"></span><span id="_______formatstring______"></span><span id="_______FORMATSTRING______"></span> *FormatString*   
指定格式的字符串，作为**printf**。 一般情况下，转换字符工作方式与 C.完全相同浮点转换字符中，64 位参数被解释为 32 位浮点数除非**l**使用修饰符。

可以添加"I64"修饰符以指示应将值解释为 64 位。 例如，"%i64x"可用于打印的 64 位十六进制数字。

支持 %p 转换字符，但它表示目标的虚拟地址空间中的指针。 不能有任何修饰符，并使用调试器的内部地址格式。 除标准的 printf 样式格式说明符，还支持以下其他转换字符。

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
<th align="left">自变量类型</th>
<th align="left">参数</th>
<th align="left">打印的文本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%p</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的指针。</p></td>
<td align="left"><p>指针的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%N</p></td>
<td align="left"><p>DWORD_PTR （32 位或 64 位，具体取决于主机的体系结构）</p></td>
<td align="left"><p>主机的虚拟地址空间中的指针。</p></td>
<td align="left"><p>指针的值。 （这等效于标准 C %p 字符。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%ma</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的以 NULL 结尾的 ASCII 字符串的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%mu</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的 NULL 终止的 Unicode 字符串的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%msa</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ANSI_STRING 结构目标的虚拟地址空间中的地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%msu</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的 UNICODE_STRING 结构地址。</p></td>
<td align="left"><p>指定的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%y</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的调试器符号的地址。</p></td>
<td align="left"><p>包含指定的符号 （和偏移量，如果有） 的名称的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%ly</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>目标的虚拟地址空间中的调试器符号的地址。</p></td>
<td align="left"><p>包含名称的指定符号 （和偏移量，如果有），以及任何可用的源行信息的字符串。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Arguments______"></span><span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *自变量*   
为指定参数的格式字符串，如**printf**。 指定的参数数目应与匹配的转换中的字符数*FormatString*。 每个自变量是将默认表达式计算器 （MASM 或 c + +） 计算的表达式。 有关详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

可以使用选择的颜色设置*选项*参数默认情况下所有设置为白色背景上的黑色文本。 若要充分利用这些选项，必须先使用[视图 |选项](view---options.md)以打开选项对话框并更改的调试器命令窗口消息的颜色设置。

下面的示例演示如何在格式字符串中包含的 DML 标记。

```dbgcmd
.printf /D "Click <link cmd=\".chain /D\">here</link> to see extensions DLLs."
```

![dml 命令浏览器窗口中的链接的屏幕截图](images/printf01.png)

在上图中所示的输出具有可单击以执行该命令中指定的链接`<link>`标记。 下图显示单击的链接的结果。

![命令浏览器窗口中的 dml 输出的屏幕截图](images/printf02.png)

有关 DML 标记的信息，请参阅有关 Windows 调试工具的 dml.doc 安装文件夹中的。

 

 





