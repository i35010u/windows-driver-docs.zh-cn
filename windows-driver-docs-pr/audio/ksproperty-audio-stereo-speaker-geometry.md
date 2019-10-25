---
title: KSPROPERTY\_音频\_立体声\_扬声器\_几何
description: KSPROPERTY\_音频\_立体声\_扬声器\_GEOMETRY 属性与 KSPROPERTY\_音频\_信道\_配置结合使用，以实现的 DirectSound 扬声器配置属性硬件加速3D 音频。
ms.assetid: 4a870368-6a9b-41bc-80c3-da6ad1f2454b
keywords:
- KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ddc30c82fe4ede557a1cea6b9c51cf8ac80b2a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830936"
---
# <a name="ksproperty_audio_stereo_speaker_geometry"></a>KSPROPERTY\_音频\_立体声\_扬声器\_几何


KSPROPERTY\_音频\_立体声\_扬声器\_GEOMETRY 属性与[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)结合使用，以实现 DirectSound 发言人-配置属性用于硬件加速3D 音频。 这是 DAC 节点（[**KSNODETYPE\_dac**](ksnodetype-dac.md)）和3d 节点（[**KSNODETYPE\_3d\_效果**](ksnodetype-3d-effects.md)）的可选属性。

## <span id="ddk_ksproperty_audio_stereo_speaker_geometry_ks"></span><span id="DDK_KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY_KS"></span>


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
<td align="left"><p>固定/筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 LONG，指定扬声器几何。 此值可以设置为以下常量之一，这些常量在头文件 Ksmedia 中定义：

-   KSAUDIO\_立体声\_扬声器\_几何\_耳机

-   KSAUDIO\_立体声\_扬声器\_几何\_最小值

-   KSAUDIO\_立体声\_音箱\_几何\_窄

-   KSAUDIO\_立体声\_扬声器\_几何\_宽

-   KSAUDIO\_立体声\_扬声器\_几何\_最大

前面的参数在含义（但不等于值）中等效于以下值，这些值由**IDirectSound：： GetSpeakerConfig**方法使用（请参见 Microsoft Windows SDK 文档），并在头文件 Dsound 中定义：

-   DSSPEAKER\_耳机

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何\_分钟

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何\_窄

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何\_宽

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何\_最大值

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_立体声\_扬声器\_GEOMETRY 属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 将 KSPROPERTY\_音频\_立体声\_扬声器\_几何图形作为 DAC 节点上的筛选器属性，并作为3D 节点上的固定属性。

有关其他信息，请参阅[DirectSound 演讲者-配置设置](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-speaker-configuration-settings)。

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


[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






