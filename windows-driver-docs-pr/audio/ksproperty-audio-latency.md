---
title: KSPROPERTY \_ 音频 \_ 延迟
description: "\"KSPROPERTY \\_ 音频 \\_ 延迟\" 属性用于报告与流关联的 (或音频缓冲) 数量的延迟。"
ms.assetid: d155e3a5-e3e6-4381-9bbe-2a16b0be47b3
keywords:
- KSPROPERTY_AUDIO_LATENCY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LATENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1fe66b6e153fbf0ed4b067d41d2ec37358de0ee
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102646"
---
# <a name="ksproperty_audio_latency"></a>KSPROPERTY \_ 音频 \_ 延迟


"KSPROPERTY \_ 音频 \_ 延迟" 属性用于报告与流关联的 (或音频缓冲) 数量的延迟。

## <span id="ddk_ksproperty_audio_latency_ks"></span><span id="DDK_KSPROPERTY_AUDIO_LATENCY_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kstime" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kstime)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定流滞后时间的 KSTIME 类型的结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 延迟属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于查询 AEC 筛选器上的 pin 的流延迟。 有关详细信息，请参阅 [公开硬件加速捕获效果](./exposing-hardware-accelerated-capture-effects.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSTIME**](/windows-hardware/drivers/ddi/ks/ns-ks-kstime)

