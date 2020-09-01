---
title: KSPROPERTY \_ 音频 \_ 通道 \_ 配置
description: KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性指定节点输出的音频流中的通道的实际空间位置。
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
ms.openlocfilehash: 56c939b6747dcce2b376d8f72cc44027f60e1a09
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206973"
---
# <a name="ksproperty_audio_channel_config"></a>KSPROPERTY \_ 音频 \_ 通道 \_ 配置


KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性指定节点输出的音频流中的通道的实际空间位置。

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
<td align="left"><p>筛选器/Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config" data-raw-source="[&lt;strong&gt;KSAUDIO_CHANNEL_CONFIG&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)"><strong>KSAUDIO_CHANNEL_CONFIG</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (operation data) 的属性值是 KSAUDIO 信道 CONFIG 类型的 \_ 结构 \_ 。 此结构指定输出流中包含的通道，并将这些通道分配给扬声器。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

用作 DAC 节点的属性时 ([**KSNODETYPE \_ DAC**](ksnodetype-dac.md)) 或3D 节点 ([**KSNODETYPE \_ 三维 \_ 效果**](ksnodetype-3d-effects.md)) ，则 KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性指定 DirectSound 发言人配置。 对于立体声扬声器配置，此属性与 [**KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何**](ksproperty-audio-stereo-speaker-geometry.md) 属性结合使用，可区分耳机和几个立体声扬声器配置。 有关扬声器配置的详细信息，请参阅 [DirectSound 演讲者-配置设置](./directsound-speaker-configuration-settings.md)。

DirectSound 还使用 KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性在 "平移" 节点上查询其通道配置。 "平移节点" 是第二个卷节点 ([**KSNODETYPE \_ volume**](ksnodetype-volume.md)) ，它满足 [DirectSound 节点顺序要求](./directsound-node-ordering-requirements.md)。 Microsoft Windows SDK 文档中所述的 **IDirectSoundBuffer：： SetPan** 方法的 DirectSound 实现 () 使用平移节点的 [**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md) 属性来控制平移。

DirectSound 将 KSPROPERTY \_ AUDIO \_ 信道 \_ CONFIG 视为 DAC 节点上的筛选器属性，并将作为卷和3d 节点上的固定属性。

客户端还使用此属性来选择 [**KSNODETYPE \_ PROLOGIC \_ 解码器**](ksnodetype-prologic-decoder.md) 节点输出流的格式。

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


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSAUDIO \_ 通道 \_ 配置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)

[**KSNODETYPE \_ DAC**](ksnodetype-dac.md)

[**KSNODETYPE \_ 三维 \_ 效果**](ksnodetype-3d-effects.md)

[**KSNODETYPE \_ 卷**](ksnodetype-volume.md)

[**KSNODETYPE \_ PROLOGIC \_ 解码器**](ksnodetype-prologic-decoder.md)

[**KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

