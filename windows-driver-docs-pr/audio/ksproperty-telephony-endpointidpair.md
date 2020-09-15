---
title: KSPROPERTY \_ 电话服务 \_ ENDPOINTIDPAIR
description: KSPROPERTY \_ 电话服务 \_ ENDPOINTIDPAIR 属性包含移动电话音频路由的呈现和捕获终结点。
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
ms.openlocfilehash: b22f76754b366b7e6ea5a0cc8a33b70c33d86108
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101846"
---
# <a name="ksproperty_telephony_endpointidpair"></a>KSPROPERTY \_ 电话服务 \_ ENDPOINTIDPAIR


**KSPROPERTY \_ 电话服务 \_ ENDPOINTIDPAIR**属性包含移动电话音频路由的呈现和捕获终结点。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTIDPAIR&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)"><strong>KSTOPOLOGY_ENDPOINTIDPAIR</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 [**KSTOPOLOGY \_ ENDPOINTIDPAIR**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)，它指定呈现和捕获终结点。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ 电话服务 \_ ENDPOINTIDPAIR**属性请求返回手机网络音频路由的呈现和捕获终结点。

<a name="remarks"></a>注解
-------

通过拓扑筛选器上的 **KSPROPERTY \_ 电话服务 \_ ENDPOINTIDPAIR** 属性控制手机网络路由。 此属性为所请求的终结点组合使用一对 [**KSTOPOLOGY \_ ENDPOINTID**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid) 结构。 **KSTOPOLOGY \_ENDPOINTID** 包含终结点的拓扑筛选器的引用字符串，以及终结点连接到的拓扑筛选器 PIN ID。 驱动程序提供对此属性的基本支持，并返回可用于移动电话音频路由的所有有效的呈现对和捕获终结点。 驱动程序负责处理将移动电话和捕获移动电话音频移动到这个新的终结点组合，满足硬件所需的任何约束。 即使系统中没有活动电话呼叫，也必须可以设置此属性。

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

