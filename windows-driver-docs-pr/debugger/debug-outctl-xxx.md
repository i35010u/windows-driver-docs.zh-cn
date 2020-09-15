---
title: 调试 \_ OUTCTL \_ XXX
description: DEBUG \_ OUTCTL \_ XXX 常量用于输出控制。 常量构成一个位域，该字段指定发送输出的目标的当前策略。 位域分为两部分。
ms.assetid: 94d3416a-082e-488b-adc2-8b837bb1c1cb
ms.date: 12/07/2017
keywords:
- DEBUG_OUTCTL_XXX Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_OUTCTL_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: b11cea884064d6adcc1c46c560ebd2678f23dc7b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103854"
---
# <a name="debug_outctl_xxx"></a>调试 \_ OUTCTL \_ XXX


DEBUG \_ OUTCTL \_ *XXX*常量用于输出控制。 常量构成一个位域，该字段指定发送输出的目标的当前策略。 位域分为两部分。

## <span id="ddk_debug_outctl_xxx_dbx"></span><span id="DDK_DEBUG_OUTCTL_XXX_DBX"></span>


较低位必须是下列值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_THIS_CLIENT</p></td>
<td align="left"><p>由该客户端调用的方法生成的输出将仅发送到此客户端的 <a href="/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks" data-raw-source="[output callbacks](./using-input-and-output.md#output-callbacks)">输出回调</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_ALL_CLIENTS</p></td>
<td align="left"><p>输出将发送到所有客户端。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_ALL_OTHER_CLIENTS</p></td>
<td align="left"><p>输出将发送到 (除了生成输出) 的客户端之外的所有客户端。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_IGNORE</p></td>
<td align="left"><p>输出将立即被丢弃，且不会被记录或发送到回调。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_LOG_ONLY</p></td>
<td align="left"><p>将记录输出，但不会将其发送到回调。</p></td>
</tr>
</tbody>
</table>

 

位域的更高位可能包含以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_NOT_LOGGED</p></td>
<td align="left"><p>不要将此客户端的输出放入全局日志文件中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_OVERRIDE_MASK</p></td>
<td align="left"><p>无论客户端的输出掩码是否允许，都将输出发送到客户端。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_DML</p></td>
<td align="left"><p>对于支持调试器标记语言 (DML) 的输出，将以 DML 格式发送输出。</p></td>
</tr>
</tbody>
</table>

 

若要创建有效的输出控件位字段，请从第一个表中提取一个值，并在第二个表中使用零个或更多值，并使用按位 "或" 运算符合并它们。

输出控件位字段的默认值为 DEBUG \_ OUTCTL \_ 所有 \_ 客户端。

作为创建自己的输出控件位字段的替代方法，可以使用以下值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_DML</p></td>
<td align="left"><p>将新的输出控件设置为与当前输出控件相同的值，并指定输出将为 DML 格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_TEXT</p></td>
<td align="left"><p>将新的输出控件设置为与当前输出控件相同的值，并指定输出将为文本格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT</p></td>
<td align="left"><p>与 DEBUG_OUTCTL_AMBIENT_TEXT 相同。</p></td>
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

