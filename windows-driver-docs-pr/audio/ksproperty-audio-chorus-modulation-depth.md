---
title: KSPROPERTY \_ 音频 \_ CHORUS \_ 调制 \_ 深度
description: KSPROPERTY \_ AUDIO \_ CHORUS \_ 调制 \_ depth 属性指定 CHORUS 的调制深度。 这是 chorus 节点 (KSNODETYPE chorus) 的属性 \_ 。
keywords:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bbead27b2a56c0fa55fdd62a33ffd542ae46949
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784549"
---
# <a name="ksproperty_audio_chorus_modulation_depth"></a>KSPROPERTY \_ 音频 \_ CHORUS \_ 调制 \_ 深度


KSPROPERTY \_ AUDIO \_ CHORUS \_ 调制 \_ depth 属性指定 CHORUS 的调制深度。 这是 chorus 节点 ([**KSNODETYPE \_ chorus**](ksnodetype-chorus.md)) 的属性。

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
<td align="left"><p>KSNODEPROPERTY</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值为 ULONG 类型，它指定 chorus 的调制深度。 它以毫秒为单位表示，并设置调制器的速度 (频率) 。 该值的范围是从0到255.9961，以 1/256th 为增量。 为此，应将属性值表示为固定点16.16 值，其中以下为 true：

-   值0x00010000 表示1毫秒
-   值0xFFFFFFFF 表示 (65536-1/65536) ms

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 CHORUS 的 " \_ 深度" \_ \_ 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE \_ CHORUS**](ksnodetype-chorus.md)

 

 






