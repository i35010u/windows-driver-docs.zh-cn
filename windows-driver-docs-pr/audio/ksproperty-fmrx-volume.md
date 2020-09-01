---
title: KSPROPERTY \_ FMRX \_
description: KSPROPERTY \_ FMRX \_ volume 属性控制调频广播的音量。
ms.assetid: 28650DEB-EA09-4E30-A1A7-179D1E1A641F
keywords:
- KSPROPERTY_FMRX_VOLUME 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b7fa1ee81456d77dd4f158c5501abcb7fef9b64
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210983"
---
# <a name="ksproperty_fmrx_volume"></a>KSPROPERTY \_ FMRX \_


**KSPROPERTY \_ FMRX \_ VOLUME**属性控制调频广播的音量。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 LONG，并指定 FM 无线音量。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ FMRX \_ volume**属性请求返回调频无线电量。

<a name="remarks"></a>备注
-------

FM volume 和路由 (终结点选择) 由拓扑筛选器上的 **KSPROPERTY \_ FMRX \_ volume** 和 [**KSPROPERTY \_ FMRX \_ ENDPOINTID**](ksproperty-fmrx-endpointid.md) 属性控制。 **KSPROPERTY \_ FMRX \_ volume**属性的基本支持应返回最小卷、最大卷和卷范围。

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

 

