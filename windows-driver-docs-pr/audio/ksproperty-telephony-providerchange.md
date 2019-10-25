---
title: KSPROPERTY\_电话\_PROVIDERCHANGE
description: KSPROPERTY\_电话服务\_PROVIDERCHANGE 属性用于与音频驱动程序通信，即无线电语音呼叫连续性（SRVCC）正在开始或结束。
ms.assetid: 9CEDAFE7-014F-4670-958D-6D3687D2D24A
keywords:
- KSPROPERTY_TELEPHONY_PROVIDERCHANGE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_PROVIDERCHANGE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c0f6c69d1c9573c5a049be517db988d03dc5ff4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832688"
---
# <a name="ksproperty_telephony_providerchange"></a>KSPROPERTY\_电话\_PROVIDERCHANGE


**KSPROPERTY\_电话服务\_PROVIDERCHANGE**属性用于与音频驱动程序通信，即无线电语音呼叫连续性（SRVCC）正在开始或结束。

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
<td align="left"><p>无</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange" data-raw-source="[&lt;strong&gt;KSTELEPHONY_PROVIDERCHANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)"><strong>KSTELEPHONY_PROVIDERCHANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值的类型为[**KSTELEPHONY\_PROVIDERCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)，它指定电话呼叫类型和提供程序更改操作的类型。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_电话服务\_PROVIDERCHANGE**属性请求返回状态\_SUCCESS，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频堆栈使用[**KSTELEPHONY\_PROVIDERCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)属性来指示 SRVCC 与音频驱动程序的开头和结尾。 此属性将呼叫类型（LTE 数据包交换、WLAN 数据包交换或线路交换）与提供程序更改操作（开始、结束或取消）传递给驱动程序。 当提供程序操作用于结束 SRVCC 时，调用类型将被忽略。

当提供程序更改操作为**电话服务\_PROVIDERCHANGEOP\_开始**时，驱动程序会将该提供程序的调用状态更新为**电话服务\_CALLSTATE\_PROVIDERTRANSITION**。 当提供程序更改操作为**电话服务\_PROVIDERCHANGEOP\_结束**时，驱动程序会将该提供程序的调用状态更新为**电话服务\_CALLSTATE\_启用**。 在 SRVCC 期间，驱动程序必须继续使用关联的[**KSNODETYPE\_电话\_双向**](ksnodetype-telephony-bidi.md)终结点，并且不会更改此终结点的插孔状态。 如果提供程序更改操作为**电话服务\_PROVIDERCHANGEOP\_"取消**"，则将取消 SRVCC，驱动程序应还原为预 SRVCC 调用。

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

 

 





