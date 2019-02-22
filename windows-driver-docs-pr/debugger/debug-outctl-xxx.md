---
title: DEBUG\_OUTCTL\_XXX
description: 调试\_OUTCTL\_XXX 常量用于输出控制。 常量构成一个位字段，指定将输出发送到何处的当前策略。 位域被划分为两个部分。
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
ms.openlocfilehash: 0886488bbb8b812a0507e6b83dc54204a23fbd82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532946"
---
# <a name="debugoutctlxxx"></a>DEBUG\_OUTCTL\_XXX


调试\_OUTCTL\_*XXX*常量用于输出控制。 常量构成一个位字段，指定将输出发送到何处的当前策略。 位域被划分为两个部分。

## <span id="ddk_debug_outctl_xxx_dbx"></span><span id="DDK_DEBUG_OUTCTL_XXX_DBX"></span>


较低的位必须正好是以下值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_THIS_CLIENT</p></td>
<td align="left"><p>通过此客户端调用的方法由生成输出将只发送到此客户端&#39;s<a href="https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks" data-raw-source="[output callbacks](https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks)">输出回调</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_ALL_CLIENTS</p></td>
<td align="left"><p>输出将发送到所有客户端。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_ALL_OTHER_CLIENTS</p></td>
<td align="left"><p>输出将发送到所有客户端 （到生成输出的客户端除外）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_IGNORE</p></td>
<td align="left"><p>输出将被立即放弃并不会记录或发送到回调。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_LOG_ONLY</p></td>
<td align="left"><p>输出将记录，但不是会发送到回调。</p></td>
</tr>
</tbody>
</table>

 

位域的更高版本位可能包含以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_NOT_LOGGED</p></td>
<td align="left"><p>不要将输出放在从此客户端全局日志文件中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_OVERRIDE_MASK</p></td>
<td align="left"><p>将输出发送到客户端，而不管是否在客户端&#39;s 输出掩码允许它。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_DML</p></td>
<td align="left"><p>对于支持调试器标记语言 (DML) 的输出，DML 格式发送输出。</p></td>
</tr>
</tbody>
</table>

 

若要创建一个有效的输出控件位字段，采用从第一个表，以及从第二个表中的零个或多个值的一个值，并使用按位 OR 运算符合并它们。

输出控制位域的默认值为 DEBUG\_OUTCTL\_所有\_客户端。

作为创建您自己输出控制位域的替代方法，可以使用以下值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_DML</p></td>
<td align="left"><p>将新的输出控制设置为与当前的输出控件相同的值，并指定的输出将以 DML 格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_TEXT</p></td>
<td align="left"><p>将新的输出控制设置为与当前的输出控件相同的值，并指定的输出将以文本格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT</p></td>
<td align="left"><p>传递 DEBUG_OUTCTL_AMBIENT_TEXT 相同。</p></td>
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
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

 

 





