---
title: KSPROPERTY\_电话\_CALLHOLD
description: KSPROPERTY\_电话\_CALLHOLD 属性用于控制电话呼叫的保留状态。
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
ms.openlocfilehash: f3274d81de9894e166b574581f3357d4ddc9f5b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832712"
---
# <a name="ksproperty_telephony_callhold"></a>KSPROPERTY\_电话\_CALLHOLD


**KSPROPERTY\_电话\_CALLHOLD**属性用于控制电话呼叫的保留状态。

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 BOOL 并指定电话呼叫是否处于暂停状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果中的调用处于暂停状态，则**KSPROPERTY\_电话服务\_CALLHOLD**属性请求返回**TRUE** ;否则，返回**FALSE**。

<a name="remarks"></a>备注
-------

如果将**KSPROPERTY\_电话服务\_CALLHOLD**属性的值设置为**TRUE**，则会将电话呼叫置于保持状态。 预期的行为是传输和接收都将静音。 在这种情况下，将不会发送或接收任何数据。 音频驱动程序会将呼叫状态（[**电话\_CALLSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callstate)）更新为**电话服务\_CALLSTATE\_保持**。 如果将**KSPROPERTY\_电话服务\_CALLHOLD**属性的值设置为 " **FALSE**"，则会将电话设置为 "暂停" 状态，并将呼叫状态更新为 "**电话服务\_CALLSTATE"\_启用**。

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
<td align="left"><p>Windows 10</p></td>
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

 

 





