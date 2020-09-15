---
title: KSPROPERTY \_ 音频 \_ 数字 \_ EQ \_ 带区
description: KSPROPERTY \_ AUDIO \_ NUM \_ EQ \_ 波段属性用于检索均衡表中的频率带区数。 这是 (KSNODETYPE 均衡器) 的 EQ 节点中通道的获取属性 \_ 。
ms.assetid: b7bb9f05-0b27-4b41-aa38-efb87fc1beee
keywords:
- KSPROPERTY_AUDIO_NUM_EQ_BANDS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_NUM_EQ_BANDS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6959c41a08898617b097fecb1f3dbb8d4d8b647c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102082"
---
# <a name="ksproperty_audio_num_eq_bands"></a>KSPROPERTY \_ 音频 \_ 数字 \_ EQ \_ 带区


KSPROPERTY \_ AUDIO \_ NUM \_ EQ \_ 波段属性用于检索均衡表中的频率带区数。 这是 ([**KSNODETYPE \_ 均衡**](ksnodetype-equalizer.md) 器) 的 EQ 节点中通道的获取属性。

## <span id="ddk_ksproperty_audio_num_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_NUM_EQ_BANDS_KS"></span>


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
<td align="left"><p>筛选器</p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，并指定节点的均衡表中的频率带区数。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 号 \_ EQ \_ 波段属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性与 [**KSPROPERTY \_ audio \_ eq \_ 带区**](ksproperty-audio-eq-bands.md) 和 [**KSPROPERTY \_ 音频 \_ eq \_ 级别**](ksproperty-audio-eq-level.md) 属性结合使用，以确定包含这些属性的值的数组的长度。

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

[**KSNODETYPE \_ 均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY \_ 音频 \_ EQ \_ 带区**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY \_ 音频 \_ EQ \_ 级别**](ksproperty-audio-eq-level.md)

