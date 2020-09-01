---
title: 调试 \_ TYPEOPTS \_ XXX
description: 类型选项会影响引擎格式化输出的数字和字符串的方式。
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
ms.openlocfilehash: 377d832a259dc3ed178ea930c4f2ccae7b8a85a1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213035"
---
# <a name="debug_typeopts_xxx"></a>调试 \_ TYPEOPTS \_ XXX


类型选项会影响引擎格式化输出的数字和字符串的方式。

选项由具有以下位标志的位集表示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回的常量</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_TYPEOPTS_UNICODE_DISPLAY"></span><span id="debug_typeopts_unicode_display"></span>
<strong>DEBUG_TYPEOPTS_UNICODE_DISPLAY</strong></td>
<td align="left"><p>设置此位后，USHORT 指针和数组作为 Unicode 字符输出。</p>
<p>这等效于调试器命令 <strong>。 enable_unicode 1</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY"></span><span id="debug_typeopts_longstatus_display"></span>
<strong>DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY</strong></td>
<td align="left"><p>设置此位后，长整数将输出为默认的基数，而不是十进制。</p>
<p>这等效于调试器命令 <strong>。 enable_long_status 1</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_TYPEOPTS_FORCERADIX_OUTPUT"></span><span id="debug_typeopts_forceradix_output"></span>
<strong>DEBUG_TYPEOPTS_FORCERADIX_OUTPUT</strong></td>
<td align="left"><p>设置此位时，整数 (除了长整数外) ，将输出默认的基数而不是 decimal。</p>
<p>这等效于调试器命令 <strong>。 force_radix_output 1</strong>。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

默认情况下，所有类型格式设置选项都处于关闭状态。

有关类型的详细信息，请参阅 [类型](./types.md)。

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

 

