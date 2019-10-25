---
title: KSPROPERTY\_音频\_POSITIONEX
description: KSPROPERTY\_音频\_POSITIONEX 属性为调用方提供基于内核流式处理（KS）的音频驱动程序的流位置和关联时间戳信息。
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
ms.openlocfilehash: e17680a0e114e77e111aac06814a4a0517d8ac03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832944"
---
# <a name="ksproperty_audio_positionex"></a>KSPROPERTY\_音频\_POSITIONEX


KSPROPERTY\_音频\_POSITIONEX 属性为调用方提供基于内核流式处理（KS）的音频驱动程序的流位置和关联时间戳信息。

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
<td align="left"><p>无</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITIONEX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)"><strong>KSAUDIO_POSITIONEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是\_KSAUDIO POSITIONEX 类型的结构，该结构接收来自属性处理程序的位置信息。 KSAUDIO\_POSITIONEX 结构指定的位置信息是调用方所选的 pin 的位置信息。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

如果调用成功，则 KSPROPERTY\_音频\_POSITIONEX 属性请求返回\_OK。 否则，它将返回相应的 HRESULT 错误代码。

<a name="remarks"></a>备注
-------

通常，音频应用程序必须监视音频流的当前位置。 此位置被指定为距流开头的字节偏移量。 流位置信息有两种可能的解释：

-   对于呈现流，流位置是当前通过数字到模拟转换器（Dac）播放的音频帧的字节偏移量。

-   对于捕获流，流位置是当前通过模拟到数字转换器（ADCs）记录的音频帧的字节偏移量。

支持 KSPROPERTY\_音频\_POSITIONEX 属性的驱动程序为流位置值生成时间戳窗口。 时间戳窗口是在确定流位置之前采样的时间戳和确定流位置后拍摄的时间戳之间的时间间隔。 然后，调用方确定它是否可以使用 "时间戳" 窗口。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIO\_POSITIONEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






