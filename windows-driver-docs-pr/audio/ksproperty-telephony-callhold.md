---
title: KSPROPERTY \_ 电话服务 \_ CALLHOLD
description: KSPROPERTY \_ \_ phone CALLHOLD 属性用于控制电话呼叫的保留状态。
ms.assetid: C683A6AA-35E5-43D3-B882-B13B8A0A4043
keywords:
- KSPROPERTY_TELEPHONY_CALLHOLD 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_CALLHOLD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89f12f3d54408db326df0930ece167d50defd1f0
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101856"
---
# <a name="ksproperty_telephony_callhold"></a>KSPROPERTY \_ 电话服务 \_ CALLHOLD


**KSPROPERTY phone \_ \_ CALLHOLD**属性用于控制电话呼叫的保留状态。

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
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 BOOL 并指定电话呼叫是否处于暂停状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果中的调用处于开启状态，则 **KSPROPERTY \_ 电话服务 \_ CALLHOLD** 属性请求返回 **TRUE** ; 否则返回 **FALSE**。

<a name="remarks"></a>备注
-------

如果将 KSPROPERTY phone ** \_ \_ CALLHOLD** 属性的值设置为 **TRUE**，则会将电话呼叫置于保持状态。 预期的行为是传输和接收都将静音。 在这种情况下，将不会发送或接收任何数据。 音频驱动程序会将电话 CALLSTATE)  ([**电话 \_ 服务**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callstate) 更新为 **电话服务 \_ CALLSTATE \_ 暂**留。 如果将 " **KSPROPERTY" \_ 电话 \_ 服务** 的 "CALLHOLD" 属性设置为 " **FALSE**"，则会将电话设置为 "暂停" 状态，并将呼叫状态更新为 " ** \_ \_ 已启用电话服务 CALLSTATE**"。

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

