---
title: 调试 \_ 符号 \_ XXX
description: DEBUG \_ 符号 \_ XXX 常量用于符号标志位集。 符号标志描述符号组中符号) 部分 (。
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- DEBUG_SYMBOL_EXPANDED
- DEBUG_SYMBOL_READ_ONLY
- DEBUG_SYMBOL_IS_ARRAY
- DEBUG_SYMBOL_IS_FLOAT
- DEBUG_SYMBOL_IS_ARGUMENT
- DEBUG_SYMBOL_IS_LOCAL
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 429ad5a94acaf12635a232bef13a0b5265caf05f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838827"
---
# <a name="debug_symbol_xxx"></a>调试 \_ 符号 \_ XXX


DEBUG \_ 符号 \_ *XXX* 常量用于符号标志位集。 符号标志描述符号组中符号) 部分 (。

符号标志的最小有效位-在 "调试符号展开级别掩码" 中找到的位数 \_ \_ \_ \_ ，表示符号组内符号的展开深度。 子符号的深度始终比其父符号的深度多一个。 例如，若要查找其标志包含在变量 *标志* 中的符号深度，请使用以下语句：

```dbgcmd
depth = flags & DEBUG_SYMBOL_EXPANSION_LEVEL_MASK;
```

符号标志的其余位集可以包含以下位标志。

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
<td align="left"><span id="DEBUG_SYMBOL_EXPANDED"></span><span id="debug_symbol_expanded"></span>
<strong>DEBUG_SYMBOL_EXPANDED</strong></td>
<td align="left"><p>符号的子级是符号组的一部分。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_READ_ONLY"></span><span id="debug_symbol_read_only"></span>
<strong>DEBUG_SYMBOL_READ_ONLY</strong></td>
<td align="left"><p>符号表示只读变量。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_SYMBOL_IS_ARRAY"></span><span id="debug_symbol_is_array"></span>
<strong>DEBUG_SYMBOL_IS_ARRAY</strong></td>
<td align="left"><p>符号表示数组变量。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_IS_FLOAT"></span><span id="debug_symbol_is_float"></span>
<strong>DEBUG_SYMBOL_IS_FLOAT</strong></td>
<td align="left"><p>符号表示浮点变量。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_SYMBOL_IS_ARGUMENT"></span><span id="debug_symbol_is_argument"></span>
<strong>DEBUG_SYMBOL_IS_ARGUMENT</strong></td>
<td align="left"><p>符号表示传递给函数的参数。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_IS_LOCAL"></span><span id="debug_symbol_is_local"></span>
<strong>DEBUG_SYMBOL_IS_LOCAL</strong></td>
<td align="left"><p>符号表示范围中的局部变量。</p></td>
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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 符号 \_ 参数**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_parameters)

 

