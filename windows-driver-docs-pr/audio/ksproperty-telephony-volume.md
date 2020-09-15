---
title: KSPROPERTY \_ 电话 \_ 卷
description: "\"KSPROPERTY \\_ 电话\" \\_ 卷属性用于控制所有手机呼叫的卷。"
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
ms.openlocfilehash: 392d6ee9b1b4ee00c73eabd93be97731e8d0aca6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101824"
---
# <a name="ksproperty_telephony_volume"></a>KSPROPERTY \_ 电话 \_ 卷


" **KSPROPERTY \_ 电话" \_ 卷** 属性用于控制所有手机呼叫的卷。

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
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 LONG，并指定移动电话呼叫量。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ 电话服务 \_ 卷**属性请求返回手机网络呼叫量。

<a name="remarks"></a>备注
-------

对于手机网络呼叫，只有此卷适用于手机网络数据，并且终结点卷不起作用。 即使系统中没有活动电话呼叫，也必须可以设置此属性。 此属性的基本支持应返回最小卷、最大卷和卷范围。

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

