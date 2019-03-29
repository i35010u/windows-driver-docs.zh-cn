---
title: KSPROPERTY\_音频\_通道\_配置
description: KSPROPERTY\_音频\_通道\_CONFIG 属性节点输出音频流中指定的通道的实际空间位置。
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
ms.openlocfilehash: 88f79c93576ee5f8dccfd4610e459919eb8b5587
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563376"
---
# <a name="kspropertyaudiochannelconfig"></a>KSPROPERTY\_音频\_通道\_配置


KSPROPERTY\_音频\_通道\_CONFIG 属性节点输出音频流中指定的通道的实际空间位置。

## <span id="ddk_ksproperty_audio_channel_config_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHANNEL_CONFIG_KS"></span>


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
<td align="left"><p>筛选器/Pin</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537083" data-raw-source="[&lt;strong&gt;KSAUDIO_CHANNEL_CONFIG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537083)"><strong>KSAUDIO_CHANNEL_CONFIG</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_通道\_配置。 此结构指定包含在输出流和分配到扬声器这些通道的通道。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_通道\_配置属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

当用作 DAC 节点的属性 ([**KSNODETYPE\_DAC**](ksnodetype-dac.md)) 或三维的节点 ([**KSNODETYPE\_3D\_效果** ](ksnodetype-3d-effects.md))，KSPROPERTY\_音频\_通道\_配置属性指定 DirectSound 扬声器配置。 对于立体声扬声器配置，使用此属性与结合[ **KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY** ](ksproperty-audio-stereo-speaker-geometry.md)属性，用于区分耳机和几个立体声扬声器配置。 有关扬声器配置的详细信息，请参阅[DirectSound 扬声器配置设置](https://msdn.microsoft.com/library/windows/hardware/ff536332)。

DirectSound 还使用 KSPROPERTY\_音频\_通道\_要查询其通道配置的"平移"节点的配置属性。 平移节点是第二个卷节点 ([**KSNODETYPE\_卷**](ksnodetype-volume.md)) 满足对 mixer pin [DirectSound 节点排序要求](https://msdn.microsoft.com/library/windows/hardware/ff536331)。 DirectSound 实现**IDirectSoundBuffer::SetPan** （Microsoft Windows SDK 文档中所述） 的方法使用平移节点[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](ksproperty-audio-volumelevel.md)属性来控制平移。

DirectSound 将 KSPROPERTY\_音频\_通道\_配置为在 DAC 节点上，筛选器属性和作为卷和 3D 节点上的固定属性。

客户端还使用此属性用于选择流的格式， [ **KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)输出节点。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSAUDIO\_通道\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff537083)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_EFFECTS**](ksnodetype-3d-effects.md)

[**KSNODETYPE\_卷**](ksnodetype-volume.md)

[**KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)

[**KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY\_音频\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 






