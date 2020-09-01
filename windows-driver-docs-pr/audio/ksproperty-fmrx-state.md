---
title: KSPROPERTY \_ FMRX \_ 状态
description: KSPROPERTY \_ FMRX \_ STATE 属性指定是否启用调频无线电。
ms.assetid: A975221C-3300-4A44-9E8C-9AB4B4C54C32
keywords:
- KSPROPERTY_FMRX_STATE 音频设备
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
ms.openlocfilehash: 93eb083b1e2675bb2ac81e2a39887a470cc22346
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210985"
---
# <a name="ksproperty_fmrx_state"></a>KSPROPERTY \_ FMRX \_ 状态


**KSPROPERTY \_ FMRX \_ STATE**属性指定是否启用调频无线电。

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

 

属性值的类型为 BOOL，并指定是否启用调频无线电。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果启用调频无线电， **KSPROPERTY \_ FMRX \_ 状态** 属性请求将返回 **TRUE;** 如果禁用调频无线电，则返回 **FALSE** 。

<a name="remarks"></a>备注
-------

可以通过在 wave 滤镜上设置 **KSPROPERTY \_ FMRX \_ STATE** 属性来启用或禁用调频广播。 FM volume 和路由 (终结点选择) 由拓扑筛选器上的 [**KSPROPERTY \_ FMRX \_ volume**](ksproperty-fmrx-volume.md) 和 [**KSPROPERTY \_ FMRX \_ ENDPOINTID**](ksproperty-fmrx-endpointid.md) 属性控制。 **KSPROPERTY \_ FMRX \_ volume**属性的基本支持应返回最小卷、最大卷和卷范围。

新的 [**KSNODETYPE \_ FM \_ RX**](ksnodetype-fm-rx.md) 拓扑节点终结点实现为系统中的任何其他音频终结点，并且它支持所有音频终结点属性。 此终结点还支持在 [KSPROPSETID \_ 插座](kspropsetid-jack.md) 属性集下定义的插座属性。 此终结点在启动时处于拔出状态。 如果驱动程序支持捕获调频广播，则启用调频广播后，此终结点将变为活动状态。 在 **KSNODETYPE \_ FM \_ RX** 拓扑节点上创建捕获 pin 后，可通过调频接收机接收音频捕获。

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

 

