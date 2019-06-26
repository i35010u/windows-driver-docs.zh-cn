---
title: KSPROPERTY\_FMRX\_STATE
description: KSPROPERTY\_FMRX\_STATE 属性指定是否启用调频广播。
ms.assetid: A975221C-3300-4A44-9E8C-9AB4B4C54C32
keywords:
- KSPROPERTY_FMRX_STATE Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4425e093e24fa183325b468f8227d6ba31954424
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391673"
---
# <a name="kspropertyfmrxstate"></a>KSPROPERTY\_FMRX\_STATE


**KSPROPERTY\_FMRX\_状态**属性指定是否启用了 FM 收音机。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值属于类型布尔值，指定是否启用调频广播。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_FMRX\_状态**属性请求将返回**TRUE**如果启用了 FM 收音机和**FALSE**如果调频广播处于禁用状态。

<a name="remarks"></a>备注
-------

可以启用或禁用通过设置调频广播**KSPROPERTY\_FMRX\_状态**批筛选器的属性。 FM 卷和路由 （终结点选择） 受[ **KSPROPERTY\_FMRX\_卷**](ksproperty-fmrx-volume.md)并[ **KSPROPERTY\_FMRX\_ENDPOINTID** ](ksproperty-fmrx-endpointid.md)拓扑筛选器的属性。 对的基本支持**KSPROPERTY\_FMRX\_卷**属性应返回最小的卷、 最大卷和卷范围。

一个新[ **KSNODETYPE\_FM\_RX** ](ksnodetype-fm-rx.md)拓扑节点终结点实现如任何其他音频的终结点是在系统中，并支持音频终结点的所有属性。 此终结点还支持下定义的插孔属性[KSPROPSETID\_Jack](kspropsetid-jack.md)属性集。 此终结点是在启动时拔出状态。 如果驱动程序支持捕获调频广播，此终结点变为活动状态时启用了 FM 收音机中。 创建一个捕获固定**KSNODETYPE\_FM\_RX**拓扑节点允许来自 FM 接收方的音频捕获。

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
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





