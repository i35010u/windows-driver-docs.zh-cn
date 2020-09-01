---
title: KSPROPERTY \_ 音频 \_ 位置
description: "\"KSPROPERTY \\_ 音频 \\_ 位置\" 属性指定 pin 的音频流的声音缓冲区中的播放和写入光标的当前位置。"
ms.assetid: 859990bc-18c0-429a-afb6-07b5adc98630
keywords:
- KSPROPERTY_AUDIO_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b0a5158d7cbf7ee693d09049b86bbb6b39385c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206933"
---
# <a name="ksproperty_audio_position"></a>KSPROPERTY \_ 音频 \_ 位置


"KSPROPERTY \_ 音频 \_ 位置" 属性指定 pin 的音频流的声音缓冲区中的播放和写入光标的当前位置。

## <span id="ddk_ksproperty_audio_position_ks"></span><span id="DDK_KSPROPERTY_AUDIO_POSITION_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)"><strong>KSAUDIO_POSITION</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 KSAUDIO 位置类型的结构 \_ ，它指定渲染流的播放和写入位置，或者捕获流的记录和读取位置。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 位置属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用 KSPROPERTY \_ 音频 \_ 位置属性实现 **IDirectSoundBuffer：： GetCurrentPosition** 和 **IDirectSoundBuffer：： SetCurrentPosition** 方法。 Windows 多媒体函数 **waveInGetPosition** 和 **waveOutGetPosition** 也使用此属性。 有关 DirectSound 和 Windows 多媒体功能的详细信息，请参阅 Microsoft Windows SDK 文档。

WaveCyclic 和 WavePci 微型端口驱动程序无需为 KSPROPERTY 音频位置实现属性处理程序， \_ \_ 因为 WaveCyclic 和 WavePci 端口驱动程序代表微型端口驱动程序来处理此属性。 若要获取捕获流中的播放位置，请使用端口驱动程序中的属性处理程序调用微型端口驱动程序的 [**IMiniportWaveCyclicStream：： GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition) 或 [**IMiniportWavePciStream：： GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition) 方法。

有关详细信息，请参阅 [音频位置属性](./audio-position-property.md)。

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSAUDIO \_ 位置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)

[**IMiniportWaveCyclicStream::GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

[**IMiniportWavePciStream::GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)

 

