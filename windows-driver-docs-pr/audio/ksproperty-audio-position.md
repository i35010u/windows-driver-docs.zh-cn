---
title: KSPROPERTY\_音频\_位置
description: KSPROPERTY\_音频\_位置属性指定 pin 的音频流的声音缓冲区中的播放和写入游标的当前位置。
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
ms.openlocfilehash: 7336945ef936002bc5337316af88626355b591f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575216"
---
# <a name="kspropertyaudioposition"></a>KSPROPERTY\_音频\_位置


KSPROPERTY\_音频\_位置属性指定 pin 的音频流的声音缓冲区中的播放和写入游标的当前位置。

## <span id="ddk_ksproperty_audio_position_ks"></span><span id="DDK_KSPROPERTY_AUDIO_POSITION_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537091" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537091)"><strong>KSAUDIO_POSITION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_指定呈现流的播放和位置或捕获流的记录写入和读取位置的位置。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_位置属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用 KSPROPERTY\_音频\_POSITION 属性来实现**IDirectSoundBuffer::GetCurrentPosition**和**IDirectSoundBuffer::SetCurrentPosition**方法。 Windows 多媒体函数**waveInGetPosition**并**waveOutGetPosition**还使用此属性。 有关 DirectSound 和 Windows 多媒体函数的详细信息，请参阅 Microsoft Windows SDK 文档。

WaveCyclic 和 WavePci 微型端口驱动程序不需要实现属性处理程序 KSPROPERTY\_音频\_定位因为 WaveCyclic 和 WavePci 端口驱动程序处理此属性代表微型端口驱动程序。 若要获取呈现流中的 play 位置或记录捕获流中的位置，端口驱动程序中的属性处理程序调用微型端口驱动程序[ **IMiniportWaveCyclicStream::GetPosition** ](https://msdn.microsoft.com/library/windows/hardware/ff536716)或[ **IMiniportWavePciStream::GetPosition** ](https://msdn.microsoft.com/library/windows/hardware/ff536727)方法。

有关详细信息，请参阅[音频 Position 属性](https://msdn.microsoft.com/library/windows/hardware/ff536211)。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAUDIO\_POSITION**](https://msdn.microsoft.com/library/windows/hardware/ff537091)

[**IMiniportWaveCyclicStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536716)

[**IMiniportWavePciStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536727)

 

 






