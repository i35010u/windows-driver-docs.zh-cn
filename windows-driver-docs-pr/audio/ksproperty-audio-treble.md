---
title: KSPROPERTY \_ 音频 \_ 高音
description: KSPROPERTY \_ 音频 \_ 高音属性为色调节点中通道指定高音级别， (KSNODETYPE \_ 声调) 。
ms.assetid: eee12fac-fbde-44d5-9172-538b9c486697
keywords:
- KSPROPERTY_AUDIO_TREBLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_TREBLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e329d8bc1a3531e1638ea8d8523db93f45aa32db
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102038"
---
# <a name="ksproperty_audio_treble"></a>KSPROPERTY \_ 音频 \_ 高音


KSPROPERTY \_ 音频 \_ 高音属性为色调节点中通道指定高音级别， ([**KSNODETYPE \_ 声调**](ksnodetype-tone.md)) 。

## <span id="ddk_ksproperty_audio_treble_ks"></span><span id="DDK_KSPROPERTY_AUDIO_TREBLE_KS"></span>


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
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值的类型为 LONG，为通道指定了高音级别设置。 高音级别的值使用以下比例：

-2147483648 是-无限大 (衰减) ，

-2147483647 是-32767.99998474 分贝 (衰减) ，

+ 2147483647 为 + 32767.99998474 分贝 (获取) 。

由整数值（2147483648到 + 2147483647）表示的分贝范围，其中

此刻度的分辨率为1/65536 分贝。

筛选器将成功指定超出筛选器范围的值，但会将该值固定到受支持的范围内。 但在后续请求中，它将返回所使用的实际值。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 高音属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>注解
-------

声调节点可以支持用于控制高音级别、中端级别、低音级别和低音增强的属性。 有关详细信息，请参阅 [**KSNODETYPE \_ 声调**](ksnodetype-tone.md)。

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


[**KSNODEPROPERTY \_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE \_ 音**](ksnodetype-tone.md)

