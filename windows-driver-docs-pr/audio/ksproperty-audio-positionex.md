---
title: KSPROPERTY \_ 音频 \_ POSITIONEX
description: KSPROPERTY \_ audio \_ POSITIONEX 属性为调用方提供流位置，并为内核流式传输 (KS 基于) 的音频驱动程序提供关联的时间戳信息。
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
ms.openlocfilehash: ff49181c0a181b509a285799d18a34d430004583
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102068"
---
# <a name="ksproperty_audio_positionex"></a>KSPROPERTY \_ 音频 \_ POSITIONEX


KSPROPERTY \_ audio \_ POSITIONEX 属性为调用方提供流位置，并为内核流式传输 (KS 基于) 的音频驱动程序提供关联的时间戳信息。

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
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITIONEX&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)"><strong>KSAUDIO_POSITIONEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSAUDIO POSITIONEX 类型的结构 \_ ，该结构接收来自属性处理程序的位置信息。 KSAUDIO POSITIONEX 结构指定的位置信息 \_ 是调用方所选的 pin 的位置信息。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_ \_ 如果调用成功，KSPROPERTY 音频 POSITIONEX 属性请求将返回 S \_ OK。 否则，它将返回相应的 HRESULT 错误代码。

<a name="remarks"></a>注解
-------

通常，音频应用程序必须监视音频流的当前位置。 此位置被指定为距流开头的字节偏移量。 流位置信息有两种可能的解释：

-   对于呈现流，流位置是当前通过数字到模拟转换器播放的音频帧的字节偏移量 (Dac) 。

-   对于捕获流，流位置是当前通过模拟到数字转换器录制的音频帧的字节偏移量 (ADCs) 。

支持 KSPROPERTY \_ AUDIO POSITIONEX 属性的驱动程序 \_ 为流位置值生成时间戳窗口。 时间戳窗口是在确定流位置之前采样的时间戳和确定流位置后拍摄的时间戳之间的时间间隔。 然后，调用方确定它是否可以使用 "时间戳" 窗口。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIO \_ POSITIONEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

