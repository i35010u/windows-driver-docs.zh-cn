---
title: KSPROPERTY\_电话\_PROVIDERID
description: KSPROPERTY\_电话\_音频驱动程序使用 PROVIDERID 属性来将批筛选器提供程序标识符相关联。
ms.assetid: A2BE85E3-068B-41C1-9791-69A929ECEC5C
keywords:
- KSPROPERTY_TELEPHONY_PROVIDERID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_PROVIDERID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 478f74769dbe29e39859badc697740c53fdd0840
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332575"
---
# <a name="kspropertytelephonyproviderid"></a>KSPROPERTY\_电话\_PROVIDERID


**KSPROPERTY\_电话\_PROVIDERID**音频驱动程序使用属性来将批筛选器提供程序标识符相关联。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>UINT</p></td>
</tr>
</tbody>
</table>

 

属性值属于类型 UINT，指定提供程序 id。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_电话\_PROVIDERID**属性请求将返回一个表示批筛选器的音频驱动程序将关联的提供程序 ID 的 UINT 值。

<a name="remarks"></a>备注
-------

单选堆栈的提供程序 ID (执行程序 ID) 和调用类型的概念 (数据包或电路交换) 电话呼叫实例连接到特定硬件路径。 此概念仍要用来与音频驱动程序通信中使用的硬件的路径。

此硬件路径将由每个提供程序发送批筛选器的属性控制。 音频驱动程序将关联到批筛选器提供程序 ID。 此外将流式处理终结点关联的移动电话上设置此提供程序 ID。 批筛选器的提供程序 ID 必须在运行时更改。 音频堆栈将通过使用查询从驱动程序的提供程序 ID **KSPROPERTY\_电话\_PROVIDERID**属性。 发现此提供程序 ID 之后，该提供程序 id 的所有调用将都发送到特定批筛选器。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>客户端</p></td>
<td align="left"><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





