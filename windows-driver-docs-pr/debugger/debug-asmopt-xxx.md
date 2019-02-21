---
title: DEBUG\_ASMOPT\_XXX
description: 调试\_ASMOPT\_XXX 常量会影响调试器引擎如何组装和拆装为目标的处理器指令。
ms.date: 08/10/2018
topic_type:
- apiref
api_name:
- DEBUG_ASMOPT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: f3f7b50a8401cd5f49e8cf80f9a99a6d43f5e4d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554944"
---
# <a name="debugasmoptxxx"></a>DEBUG\_ASMOPT\_XXX

程序集和反汇编选项会影响调试器引擎如何组装和拆装为目标的处理器指令。


选项与以下位标志的位表示。

<table>
<tr>
<th>Constant</th>
<th>描述</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_VERBOSE"></a><a id="debug_asmopt_verbose"></a><dl>
<dt><b>DEBUG_ASMOPT_VERBOSE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>当设置此位时，其他信息包含在反汇编。</p>
<p>这相当于<b>verbose</b>选项<b>.asm</b>命令。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_NO_CODE_BYTES"></a><a id="debug_asmopt_no_code_bytes"></a><dl>
<dt><b>DEBUG_ASMOPT_NO_CODE_BYTES</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>当设置此位时，在反汇编中不包括指令的原始字节。</p>
<p>这相当于<b>no_code_bytes</b>选项<b>.asm</b>命令。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_IGNORE_OUTPUT_WIDTH"></a><a id="debug_asmopt_ignore_output_width"></a><dl>
<dt><b>DEBUG_ASMOPT_IGNORE_OUTPUT_WIDTH</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>当设置此位时，调试器时格式说明在反汇编过程忽略输出显示宽度。</p>
<p>这相当于<b>ignore_output_width</b>选项<b>.asm</b>命令。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_SOURCE_LINE_NUMBER"></a><a id="debug_asmopt_source_line_number"></a><dl>
<dt><b>DEBUG_ASMOPT_SOURCE_LINE_NUMBER</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>当设置此位时，反汇编输出的每一行是加上符号信息所提供的源代码的行号。</p>
<p>这相当于<b>source_line</b>选项<b>.asm</b>命令。</p>
</td>
</tr>
</table>


**备注**

此外，值 DEBUG_ASMOPT_DEFAULT 表示程序集和反汇编选项的默认的集。 这意味着在上表中的所有选项都关闭。 



<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

 

 





