---
title: KSPROPERTY \_ 电话服务 \_ 静音 \_ TX
description: KSPROPERTY \_ 电话服务 \_ 静音 \_ TX 属性用于控制是否将从本地麦克风传输的数据静音到远程端。
ms.assetid: FB59AFB8-A11D-4E8D-9C39-131F1D807D4A
keywords:
- KSPROPERTY_TELEPHONY_MUTE_TX 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_MUTE_TX
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652912eb56c0d7fb01b94a630fe7dd609693cde0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208878"
---
# <a name="ksproperty_telephony_mute_tx"></a>KSPROPERTY \_ 电话服务 \_ 静音 \_ TX


**KSPROPERTY \_ 电话服务 \_ 静音 \_ TX**属性用于控制是否将从本地麦克风传输的数据静音到远程端。

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
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 BOOL，它指定从本地麦克风传输的数据与远程端上呈现的数据是否处于静音。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果电话呼叫处于静音， **KSPROPERTY 的 \_ 电话服务 \_ 静音 \_ TX** 属性请求将返回 **TRUE** ; 如果电话呼叫为 unmuted，则返回 **FALSE** 。

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

 

