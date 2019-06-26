---
title: DEBUG\_TYPEOPTS\_XXX
description: 类型选项会影响引擎设置数字和字符串的输出的格式。
ms.assetid: 1c39fb80-d51b-43a6-8a68-8479022baf8a
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- DEBUG_TYPEOPTS_UNICODE_DISPLAY
- DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY
- DEBUG_TYPEOPTS_FORCERADIX_OUTPUT
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 9d21d88558c00857d35f117b26adece13daa915c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361417"
---
# <a name="debugtypeoptsxxx"></a>DEBUG\_TYPEOPTS\_XXX


类型选项会影响引擎设置数字和字符串的输出的格式。

选项表示一个带以下位标志的位集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Constant</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_TYPEOPTS_UNICODE_DISPLAY"></span><span id="debug_typeopts_unicode_display"></span>
<strong>DEBUG_TYPEOPTS_UNICODE_DISPLAY</strong></td>
<td align="left"><p>设置此位，USHORT 指针和数组时，输出为 Unicode 字符。</p>
<p>这相当于调试器命令<strong>.enable_unicode 1</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY"></span><span id="debug_typeopts_longstatus_display"></span>
<strong>DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY</strong></td>
<td align="left"><p>设置此位，长整数时，默认值而不是 decimal 基中的输出。</p>
<p>这相当于调试器命令<strong>.enable_long_status 1</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_TYPEOPTS_FORCERADIX_OUTPUT"></span><span id="debug_typeopts_forceradix_output"></span>
<strong>DEBUG_TYPEOPTS_FORCERADIX_OUTPUT</strong></td>
<td align="left"><p>设置此位，（除外长整型） 的整数时，默认基而不是十进制值中的输出。</p>
<p>这相当于调试器命令<strong>.force_radix_output 1</strong>。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

默认情况下，所有格式设置选项的类型是关闭状态。

有关类型的详细信息，请参阅[类型](https://docs.microsoft.com/windows-hardware/drivers/debugger/types)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

 

 





