---
title: KSPROPERTY \_ 电话服务 \_ PROVIDERCHANGE
description: KSPROPERTY \_ 电话服务 \_ PROVIDERCHANGE 属性用于与音频驱动程序通信，该驱动程序) 在开始或结束时 (SRVCC 的无线电语音呼叫连续性。
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
ms.openlocfilehash: 61e7180f49ed19e9aa213ea020fb59ba754da213
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101838"
---
# <a name="ksproperty_telephony_providerchange"></a>KSPROPERTY \_ 电话服务 \_ PROVIDERCHANGE


**KSPROPERTY \_ 电话服务 \_ PROVIDERCHANGE**属性用于与音频驱动程序通信，该驱动程序) 在开始或结束时 (SRVCC 的无线电语音呼叫连续性。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange" data-raw-source="[&lt;strong&gt;KSTELEPHONY_PROVIDERCHANGE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)"><strong>KSTELEPHONY_PROVIDERCHANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 [**KSTELEPHONY \_ PROVIDERCHANGE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)，它指定了电话呼叫类型和提供程序更改操作的类型。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ 电话服务 \_ PROVIDERCHANGE**属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>注解
-------

音频堆栈使用 [**KSTELEPHONY \_ PROVIDERCHANGE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange) 属性指示 SRVCC 到音频驱动程序的开始和结束。 此属性将调用类型 (LTE 数据包交换、WLAN 数据包交换或线路交换) ，以及提供程序更改操作 (开始、结束或取消) 到驱动程序。 当提供程序操作用于结束 SRVCC 时，调用类型将被忽略。

当提供程序更改操作为 **电话服务 \_ PROVIDERCHANGEOP \_ 开始**时，驱动程序会将该提供程序的调用状态更新为 **电话服务 \_ CALLSTATE \_ PROVIDERTRANSITION**。 当提供程序更改操作为 **电话服务 \_ PROVIDERCHANGEOP \_ 结束**时，驱动程序会将该提供程序的调用状态更新为 ** \_ \_ 启用电话服务 CALLSTATE**。 在 SRVCC 期间，驱动程序必须继续使用关联的 [**KSNODETYPE \_ 电话 \_ 双向**](ksnodetype-telephony-bidi.md) 终结点，并且不会更改此终结点的插孔状态。 当提供程序更改操作为 **电话服务 \_ PROVIDERCHANGEOP \_ CANCEL**时，SRVCC 将被取消，并且驱动程序应还原为预 SRVCC 调用。

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

