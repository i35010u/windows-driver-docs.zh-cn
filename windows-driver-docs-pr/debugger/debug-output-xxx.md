---
title: 调试 \_ 输出 \_ XXX
description: 调试 \_ 输出 \_ XXX 常量是输出标志。 输出标志构成一个位域，该字段指示附带输出的输出类型。
ms.date: 11/13/2018
topic_type:
- apiref
api_name:
- DEBUG_OUTPUT_NORMAL
- DEBUG_OUTPUT_ERROR
- DEBUG_OUTPUT_WARNING
- DEBUG_OUTPUT_VERBOSE
- DEBUG_OUTPUT_PROMPT
- DEBUG_OUTPUT_PROMPT_REGISTERS
- DEBUG_OUTPUT_EXTENSION_WARNING
- DEBUG_OUTPUT_DEBUGGEE
- DEBUG_OUTPUT_DEBUGGEE_PROMPT
- DEBUG_OUTPUT_SYMBOLS
- DEBUG_OUTPUT_STATUS
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: ec28faedce40bf66a5e0882396af7b51af1843e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783490"
---
# <a name="debug_output_xxx"></a>调试 \_ 输出 \_ XXX


调试 \_ 输出 \_ *XXX* 常量是输出标志。 输出标志构成一个位域，该字段指示附带输出的输出类型。

可能的值包括以下各项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回的常量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_NORMAL"></span><span id="debug_output_normal"></span>
<strong>DEBUG_OUTPUT_NORMAL</strong></td>
<td align="left"><p>正常输出。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_ERROR"></span><span id="debug_output_error"></span>
<strong>DEBUG_OUTPUT_ERROR</strong></td>
<td align="left"><p>错误输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_WARNING"></span><span id="debug_output_warning"></span>
<strong>DEBUG_OUTPUT_WARNING</strong></td>
<td align="left"><p>警告。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_VERBOSE"></span><span id="debug_output_verbose"></span>
<strong>DEBUG_OUTPUT_VERBOSE</strong></td>
<td align="left"><p>其他输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_PROMPT"></span><span id="debug_output_prompt"></span>
<strong>DEBUG_OUTPUT_PROMPT</strong></td>
<td align="left"><p>提示输出。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_PROMPT_REGISTERS"></span><span id="debug_output_prompt_registers"></span>
<strong>DEBUG_OUTPUT_PROMPT_REGISTERS</strong></td>
<td align="left"><p>在 prompt 之前注册转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_EXTENSION_WARNING"></span><span id="debug_output_extension_warning"></span>
<strong>DEBUG_OUTPUT_EXTENSION_WARNING</strong></td>
<td align="left"><p>特定于扩展操作的警告。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_DEBUGGEE"></span><span id="debug_output_debuggee"></span>
<strong>DEBUG_OUTPUT_DEBUGGEE</strong></td>
<td align="left"><p>调试目标 (的输出，例如， <strong>OutputDebugString</strong> 或 <strong>DbgPrint</strong>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_DEBUGGEE_PROMPT"></span><span id="debug_output_debuggee_prompt"></span>
<strong>DEBUG_OUTPUT_DEBUGGEE_PROMPT</strong></td>
<td align="left"><p>调试目标 (所需的输入，例如， <strong>DbgPrompt</strong>) 。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_SYMBOLS"></span><span id="debug_output_symbols"></span>
<strong>DEBUG_OUTPUT_SYMBOLS</strong></td>
<td align="left"><p>符号消息 (例如， <strong>！符号干扰</strong>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_STATUS "></span><span id="debug_output_status"></span>
<strong>DEBUG_OUTPUT_STATUS </strong></td>
<td align="left"><p>用于修改状态栏的输出。</p></td>
</tr>
</tbody>
</table>

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
<td align="left">DbgEng (包含 DbgEng) </td>
</tr>
</tbody>
</table>

 

 





