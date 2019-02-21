---
title: KSPROPERTY\_FMRX\_ENDPOINTID
description: KSTOPOLOGY\_ENDPOINTID 属性包含 FM 单选输出/呈现终结点的终结点 ID。
ms.assetid: C71DA54C-069D-43F6-8107-AF109D4CA967
keywords:
- KSPROPERTY_FMRX_ENDPOINTID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_ENDPOINTID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a6f58bd1b95a0eba5ab2d600a8a7a8a56c83b49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548210"
---
# <a name="kspropertyfmrxendpointid"></a>KSPROPERTY\_FMRX\_ENDPOINTID


[ **KSTOPOLOGY\_ENDPOINTID** ](https://msdn.microsoft.com/library/windows/hardware/mt169886)属性包含 FM 单选输出/呈现终结点的终结点 ID。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169886" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169886)"><strong>KSTOPOLOGY_ENDPOINTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值为类型[ **KSTOPOLOGY\_ENDPOINTID** ](https://msdn.microsoft.com/library/windows/hardware/mt169886)和指定的名称和与调频广播的拓扑终结点的 pin ID。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_FMRX\_ENDPOINTID**属性请求返回的名称和当前的 pin ID 呈现调频广播的终结点。

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
<td align="left"><p>Windows Server 2016</p></td>
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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_FMRXTopology](kspropsetid-fmrxtopology.md)

 

 






