---
title: KSPROPERTY\_AUDIO\_POSITIONEX
description: KSPROPERTY\_音频\_POSITIONEX 属性提供的流位置和流式处理 (KS) 内核的关联的时间戳信息的调用方-基于音频驱动程序。
ms.assetid: 660b1ee9-7c52-4d95-8df9-b1c0dce320e3
keywords:
- KSPROPERTY_AUDIO_POSITIONEX 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_POSITIONEX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 801511ec90b5da361854e13658ea9d43515ffd0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555542"
---
# <a name="kspropertyaudiopositionex"></a>KSPROPERTY\_AUDIO\_POSITIONEX


KSPROPERTY\_音频\_POSITIONEX 属性提供的流位置和流式处理 (KS) 内核的关联的时间戳信息的调用方-基于音频驱动程序。

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
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537092" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITIONEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537092)"><strong>KSAUDIO_POSITIONEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_POSITIONEX 属性处理程序从接收位置信息。 KSAUDIO 由指定的位置信息\_POSITIONEX 结构是由调用方选择了 pin 的位置信息。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_POSITIONEX 属性请求返回 S\_确定如果调用成功。 否则，它返回相应的 HRESULT 错误代码。

<a name="remarks"></a>备注
-------

通常情况下，音频的应用程序必须监视的音频流的当前位置。 此位置被指定为从流开头的字节偏移量。 有两个流位置信息的可能的解释：

-   对于呈现流，流位置是通过数字模拟转换器 (Dac) 当前正在播放的音频帧的字节偏移量。

-   对于捕获流，流位置是当前正在通过模拟到数字转换器 (ADCs) 录制的音频帧的字节偏移量。

驱动程序支持 KSPROPERTY\_音频\_POSITIONEX 属性生成的流位置值的时间戳窗口。 时间戳窗口是进行采样，确定流位置之前的时间戳和确定流位置后执行的时间戳之间的间隔。 然后，调用方确定它是否可以使用时间戳窗口。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIO\_POSITIONEX**](https://msdn.microsoft.com/library/windows/hardware/ff537092)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






