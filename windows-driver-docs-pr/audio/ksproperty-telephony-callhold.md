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
ms.openlocfilehash: f6a37d2f859bda580631e761570a1082c293c3c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527016"
---
# <a name="kspropertytelephonycallhold"></a>KSPROPERTY\_电话\_CALLHOLD


**KSPROPERTY\_电话\_CALLHOLD**属性用于控制电话呼叫的保留状态。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值的类型 BOOL，并指定电话呼叫是否处于暂停状态。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_电话\_CALLHOLD**属性请求将返回**TRUE**如果中的调用上保留; 否则，它将返回**FALSE**。

<a name="remarks"></a>备注
-------

如果您设置**KSPROPERTY\_电话\_CALLHOLD**属性值为**TRUE**，电话呼叫将置于保持状态。 预期的行为是将静音传输和接收。 将发送或接收在此情况下没有数据。 音频驱动程序将更新调用状态 ([**电话\_CALLSTATE**](https://msdn.microsoft.com/library/windows/hardware/mt169896)) 到**电话\_CALLSTATE\_保存**。 如果您设置**KSPROPERTY\_电话\_CALLHOLD**属性值为**FALSE**，电话呼叫将被从保持状态，并且调用状态将更新为**电话\_CALLSTATE\_已启用**。

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

 

 





