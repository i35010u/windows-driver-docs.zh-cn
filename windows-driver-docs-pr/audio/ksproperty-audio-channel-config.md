---
title: KSPROPERTY\_音频\_通道\_配置
description: KSPROPERTY\_音频\_通道\_CONFIG 属性指定节点输出的音频流中的通道的实际空间位置。
ms.assetid: 5ce9bf4a-c84e-4d7e-8e75-896c88ec1a72
keywords:
- KSPROPERTY_AUDIO_CHANNEL_CONFIG 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHANNEL_CONFIG
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33015cf6c88cedc5f025d281cddc6a498c056232
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831069"
---
# <a name="ksproperty_audio_channel_config"></a>KSPROPERTY\_音频\_通道\_配置


KSPROPERTY\_音频\_通道\_CONFIG 属性指定节点输出的音频流中的通道的实际空间位置。

## <span id="ddk_ksproperty_audio_channel_config_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHANNEL_CONFIG_KS"></span>


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
<td align="left"><p>“是”</p></td>
<td align="left"><p>筛选器/Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config" data-raw-source="[&lt;strong&gt;KSAUDIO_CHANNEL_CONFIG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)"><strong>KSAUDIO_CHANNEL_CONFIG</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSAUDIO\_通道\_CONFIG 类型的结构。 此结构指定输出流中包含的通道，并将这些通道分配给扬声器。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_通道\_CONFIG 属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

当用作 DAC 节点（[**KSNODETYPE\_dac**](ksnodetype-dac.md)）或3d 节点（[**KSNODETYPE\_3d\_效果**](ksnodetype-3d-effects.md)）的属性时，KSPROPERTY\_音频\_通道\_CONFIG 属性指定 DirectSound 发言人configuration. 对于立体声扬声器配置，此属性与[**KSPROPERTY\_音频\_立体声\_扬声器\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)属性一起使用，可区分耳机和多个立体声扬声器配置. 有关扬声器配置的详细信息，请参阅[DirectSound 演讲者-配置设置](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-speaker-configuration-settings)。

DirectSound 还使用 KSPROPERTY\_音频\_通道\_CONFIG 属性在 "平移" 节点上查询其通道配置。 Pan 节点是混音器 pin 上的第二个卷节点（[**KSNODETYPE\_卷**](ksnodetype-volume.md)），满足[DirectSound 的节点顺序要求](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-node-ordering-requirements)。 **IDirectSoundBuffer：： SetPan**方法的 DirectSound 实现（如 Microsoft Windows SDK 文档中所述）使用平移节点的[**KSPROPERTY\_AUDIO\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)属性来控制平移。

DirectSound 将 KSPROPERTY\_音频\_通道\_CONFIG 视为 DAC 节点上的筛选器属性，并将作为卷和3D 节点上的固定属性。

客户端还使用此属性来选择[**KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)节点输出的流的格式。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSAUDIO\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)

[**KSNODETYPE\_卷**](ksnodetype-volume.md)

[**KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)

[**KSPROPERTY\_音频\_立体声\_扬声器\_几何**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY\_音频\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 






