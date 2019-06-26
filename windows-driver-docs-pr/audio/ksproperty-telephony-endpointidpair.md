---
title: KSPROPERTY\_电话\_ENDPOINTIDPAIR
description: KSPROPERTY\_电话\_ENDPOINTIDPAIR 属性包含用于移动电话音频路由的呈现和捕获终结点。
ms.assetid: 4F163A65-5572-41D0-80B2-493285E2B87B
keywords:
- KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7215e37fa0488095e32af848a2a95a7b6f9aa4e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391572"
---
# <a name="kspropertytelephonyendpointidpair"></a>KSPROPERTY\_电话\_ENDPOINTIDPAIR


**KSPROPERTY\_电话\_ENDPOINTIDPAIR**属性包含用于移动电话音频路由的呈现和捕获终结点。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTIDPAIR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)"><strong>KSTOPOLOGY_ENDPOINTIDPAIR</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值为类型[ **KSTOPOLOGY\_ENDPOINTIDPAIR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)，它指定的呈现和捕获终结点。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_电话\_ENDPOINTIDPAIR**属性请求返回的移动电话音频路由的呈现和捕获终结点。

<a name="remarks"></a>备注
-------

移动电话路由受**KSPROPERTY\_电话\_ENDPOINTIDPAIR**拓扑筛选器的属性。 此属性采用的一对[ **KSTOPOLOGY\_ENDPOINTID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstopology_endpointid)请求的终结点组合的结构。 **KSTOPOLOGY\_ENDPOINTID**包含终结点和终结点连接到拓扑筛选器 pin ID 的拓扑筛选器的引用字符串。 该驱动程序为此属性提供基本支持，并返回所有呈现器的有效对，并捕获可用于移动电话音频路由的终结点。 它负责在驱动程序处理移动同时呈现并捕获到此新的终结点组合，满足任何约束所需的硬件的移动电话音频。 即使在系统中没有任何活动的电话呼叫时，此属性必须是可设置。

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

 

 





