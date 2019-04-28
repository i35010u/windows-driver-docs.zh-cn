---
title: KSPROPERTY\_FMRX\_VOLUME
description: KSPROPERTY\_FMRX\_卷属性控制调频广播的卷。
ms.assetid: 28650DEB-EA09-4E30-A1A7-179D1E1A641F
keywords:
- KSPROPERTY_FMRX_VOLUME Audio Devices
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
ms.openlocfilehash: a06caefd922bccec83190aee6a87b6cff3c722ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332725"
---
# <a name="kspropertyfmrxvolume"></a>KSPROPERTY\_FMRX\_VOLUME


**KSPROPERTY\_FMRX\_卷**属性控制调频广播的卷。

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
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值的类型 long 类型的值，并指定 FM 单选卷。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个**KSPROPERTY\_FMRX\_卷**属性请求返回调频广播的卷。

<a name="remarks"></a>备注
-------

FM 卷和路由 （终结点选择） 受**KSPROPERTY\_FMRX\_卷**并[ **KSPROPERTY\_FMRX\_ENDPOINTID** ](ksproperty-fmrx-endpointid.md)拓扑筛选器的属性。 对的基本支持**KSPROPERTY\_FMRX\_卷**属性应返回最小的卷、 最大卷和卷范围。

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

 

 





