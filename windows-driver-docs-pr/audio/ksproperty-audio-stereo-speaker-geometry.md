---
title: KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何
description: KSPROPERTY \_ audio \_ 立体声 \_ 扬声器 \_ 几何属性可与 KSPROPERTY \_ 音频通道配置结合使用 \_ \_ ，以实现硬件加速3d 音频的 DirectSound 扬声器配置属性。
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
ms.openlocfilehash: ff125b1d332562b518d26faaad510e693b92fe08
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784467"
---
# <a name="ksproperty_audio_stereo_speaker_geometry"></a>KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何


KSPROPERTY \_ audio \_ 立体声 \_ 扬声器 \_ 几何属性可与 [**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](ksproperty-audio-channel-config.md) 结合使用，以实现硬件加速3d 音频的 DirectSound 扬声器配置属性。 这是 DAC 节点 ([**KSNODETYPE \_ DAC**](ksnodetype-dac.md)) 和3D 节点 ([**KSNODETYPE \_ 三维 \_ 效果**](ksnodetype-3d-effects.md)) 的可选属性。

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
<td align="left"><p>固定/筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值的类型为 LONG，指定扬声器几何。 此值可以设置为以下常量之一，这些常量在头文件 Ksmedia 中定义：

-   KSAUDIO \_ 立体声 \_ 扬声器 \_ 几何 \_ 耳机

-   KSAUDIO \_ 立体声 \_ 扬声器 \_ 几何 \_ 最小值

-   KSAUDIO \_ 立体声 \_ 扬声器 \_ 几何 \_ 窄

-   KSAUDIO \_ 立体声 \_ 扬声器 \_ 几何 \_ 宽

-   KSAUDIO \_ 立体声 \_ 扬声器 \_ \_ 最大几何

前面的参数是等效的，这意味着 (但不等于值) 到以下值，这些值由 **IDirectSound：： GetSpeakerConfig** 方法使用 (查看 Microsoft Windows SDK 文档) 并在头文件 Dsound 中定义：

-   DSSPEAKER \_ 耳机

-   DSSPEAKER \_ 立体声 |DSSPEAKER \_ 几何 \_ 最小值

-   DSSPEAKER \_ 立体声 |DSSPEAKER \_ 几何 \_ 窄

-   DSSPEAKER \_ 立体声 |DSSPEAKER \_ 几何 \_ 宽

-   DSSPEAKER \_ 立体声 |\_ \_ 最大 DSSPEAKER 几何

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 将 KSPROPERTY \_ 音频 \_ 立体声 \_ 发言人 \_ 几何视为 DAC 节点上的筛选器属性，并将作为3d 节点上的固定属性。

有关其他信息，请参阅 [DirectSound Speaker-Configuration 设置](./directsound-speaker-configuration-settings.md)。

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


[**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](ksproperty-audio-channel-config.md)

[**KSNODETYPE \_ DAC**](ksnodetype-dac.md)

[**KSNODETYPE \_ 三维 \_ 效果**](ksnodetype-3d-effects.md)

[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

