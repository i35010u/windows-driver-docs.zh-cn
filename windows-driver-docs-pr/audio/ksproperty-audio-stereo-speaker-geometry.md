---
title: KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY
description: KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY 属性使用结合 KSPROPERTY\_音频\_通道\_配置来实现DirectSound 硬件加速的 3D 音频扬声器配置属性。
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
ms.openlocfilehash: 543a8b6d729dc4caae6ccd6bfb4dccf0b2606e55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358881"
---
# <a name="kspropertyaudiostereospeakergeometry"></a>KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY


KSPROPERTY\_音频\_立体声\_演讲者\_结合使用 GEOMETRY 属性[ **KSPROPERTY\_音频\_通道\_CONFIG** ](ksproperty-audio-channel-config.md)以实现硬件加速的 3D 音频 DirectSound 扬声器配置属性。 此为可选属性的 DAC 的节点 ([**KSNODETYPE\_DAC**](ksnodetype-dac.md)) 和三维节点 ([**KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)).

## <span id="ddk_ksproperty_audio_stereo_speaker_geometry_ks"></span><span id="DDK_KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY_KS"></span>


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
<td align="left"><p>固定/筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 的类型 long 类型的值，并指定演讲者几何图形。 此值可以设置为标头文件 Ksmedia.h 中定义的以下常量之一：

-   KSAUDIO\_立体声\_演讲者\_GEOMETRY\_耳机

-   KSAUDIO\_立体声\_演讲者\_GEOMETRY\_最小值

-   KSAUDIO\_STEREO\_SPEAKER\_GEOMETRY\_NARROW

-   KSAUDIO\_立体声\_演讲者\_GEOMETRY\_宽

-   KSAUDIO\_立体声\_演讲者\_GEOMETRY\_最大值

上述参数是等效的含义 （但的值不相等） 为以下值，供**IDirectSound::GetSpeakerConfig**方法 （请参阅 Microsoft Windows SDK 文档） 中定义标头文件 Dsound.h:

-   DSSPEAKER\_耳机

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何图形\_最小值

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何图形\_窄

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何图形\_宽

-   DSSPEAKER\_立体声 |DSSPEAKER\_几何图形\_最大值

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 将 KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY 作为 DAC 节点上的筛选器属性和 3D 节点上的固定属性。

有关其他信息，请参阅[DirectSound 扬声器配置设置](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-speaker-configuration-settings)。

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


[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_EFFECTS**](ksnodetype-3d-effects.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






