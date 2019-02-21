---
title: KSPROPERTY\_电话\_卷
description: KSPROPERTY\_电话\_VOLUME 属性用于控制移动电话的所有调用的卷。
ms.assetid: 3754A7A0-FA50-4831-B449-DED0D3D69418
keywords:
- KSPROPERTY_TELEPHONY_VOLUME 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8911068ddd02bbf30434394ce495d554b8501d08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520242"
---
# <a name="kspropertytelephonyvolume"></a>KSPROPERTY\_电话\_卷


**KSPROPERTY\_电话\_卷**属性用于控制移动电话的所有调用的卷。

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
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值的类型 long 类型的值，并指定移动电话呼叫量。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_电话\_卷**属性请求将返回移动电话呼叫量。

<a name="remarks"></a>备注
-------

对于移动电话呼叫，仅此卷是适用于移动电话网络数据，并且终结点的卷没有影响。 即使在系统中没有任何活动的电话呼叫时，此属性必须是可设置。 基本支持此属性应返回最小的卷、 最大卷和卷范围。

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
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





