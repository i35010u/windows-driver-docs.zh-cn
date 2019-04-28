---
title: KSPROPERTY\_电话\_PROVIDERCHANGE
description: KSPROPERTY\_电话\_PROVIDERCHANGE 属性用于单个单选语音呼叫连续性 (SRVCC) 开始或结束与音频驱动程序进行通信。
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
ms.openlocfilehash: 0cc68047a87b0babae1d7cf1e80d6c751d527fa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332579"
---
# <a name="kspropertytelephonyproviderchange"></a>KSPROPERTY\_电话\_PROVIDERCHANGE


**KSPROPERTY\_电话\_PROVIDERCHANGE**属性用于单个单选语音呼叫连续性 (SRVCC) 开始或结束与音频驱动程序进行通信。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169885" data-raw-source="[&lt;strong&gt;KSTELEPHONY_PROVIDERCHANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169885)"><strong>KSTELEPHONY_PROVIDERCHANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值为类型[ **KSTELEPHONY\_PROVIDERCHANGE**](https://msdn.microsoft.com/library/windows/hardware/mt169885)，后者指定电话呼叫类型和提供程序的类型更改操作。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_电话\_PROVIDERCHANGE**属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

使用音频堆栈[ **KSTELEPHONY\_PROVIDERCHANGE** ](https://msdn.microsoft.com/library/windows/hardware/mt169885)属性以指示开始和结束 SRVCC 到音频驱动程序。 此属性进行通信的调用类型 (LTE 数据包交换 WLAN 数据包交换或电路交换式) 和提供程序更改操作 （开始、 结束或取消） 驱动程序。 对于结束 SRVCC 提供程序操作时，将忽略调用类型。

提供程序更改操作是何时**电话\_PROVIDERCHANGEOP\_开始**，该驱动程序更新到该提供程序的调用状态**电话服务\_CALLSTATE\_PROVIDERTRANSITION**。 提供程序更改操作是何时**电话\_PROVIDERCHANGEOP\_最终**，驱动程序更新到该提供程序的调用状态**电话服务\_CALLSTATE\_启用**。 在 SRVCC，驱动程序必须继续使用关联[ **KSNODETYPE\_电话\_BIDI** ](ksnodetype-telephony-bidi.md)终结点，而它不会更改此终结点的 jack 状态。 提供程序更改操作是何时**电话\_PROVIDERCHANGEOP\_取消**、 正在取消 SRVCC，并且该驱动程序应恢复为以前 SRVCC 调用。

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

 

 





