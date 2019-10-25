---
title: KSPROPERTY\_音频\_NUM\_EQ\_带区
description: KSPROPERTY\_音频\_NUM\_EQ\_波段属性用于检索均衡表中的频率带区数。 这是 EQ 节点中通道的一个 "获取" 属性（KSNODETYPE\_均衡器）。
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
ms.openlocfilehash: 1d36d46854b9493413c35ac3a04a985a4bd1265d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830968"
---
# <a name="ksproperty_audio_num_eq_bands"></a>KSPROPERTY\_音频\_NUM\_EQ\_带区


KSPROPERTY\_音频\_NUM\_EQ\_波段属性用于检索均衡表中的频率带区数。 这是 EQ 节点中通道的一个 "获取" 属性（[**KSNODETYPE\_均衡**](ksnodetype-equalizer.md)器）。

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG，并指定节点的均衡表中的频率带区数。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_NUM\_EQ\_波段属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性与[**KSPROPERTY\_音频\_EQ\_波段**](ksproperty-audio-eq-bands.md)和[**KSPROPERTY\_音频\_eq\_级别**](ksproperty-audio-eq-level.md)属性一起使用，以确定包含的值的数组的长度这些属性。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY\_音频\_频道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY\_音频\_EQ\_波段**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY\_音频\_EQ\_级别**](ksproperty-audio-eq-level.md)

 

 






