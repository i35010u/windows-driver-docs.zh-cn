---
title: KSPROPERTY\_RTAUDIO\_演示文稿\_位置
description: KSPROPERTY\_RTAUDIO\_演示文稿\_返回流表示信息的位置。
ms.assetid: 333A7432-B78A-4F61-B70D-D4F651F90AF7
keywords:
- KSPROPERTY_RTAUDIO_PRESENTATION_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_PRESENTATION_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 01/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: aaa3bc9613bd4e57d3b181015ddee9baeaeb8b3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332666"
---
# <a name="kspropertyrtaudiopresentationposition"></a>KSPROPERTY\_RTAUDIO\_演示文稿\_位置


KSPROPERTY\_RTAUDIO\_演示文稿\_返回流表示信息的位置。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_presentation_position"><STRONG>KSAUDIO_PRESENTATION_POSITION</STRONG></a></p></td>
</tr>
</tbody>
</table>
 

属性描述符 （实例数据） 是[ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)结构。 发送请求之前, 在客户端加载具有值，用于描述音频数据的流中的当前光标位置的结构。

属性值是[ **KSAUDIO\_演示文稿\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450865)结构，它表示音频的数据流中的最新的演示文稿位置。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_演示文稿\_位置属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。

<a name="remarks"></a>备注
-------

操作系统可能会定期从驱动程序以允许将与音频流同步视频或其他活动的上层从驱动程序检索最新的演示文稿位置信息中获取此属性。

在的 u64PositionInBlocks 成员中返回的值[ **KSAUDIO\_演示文稿\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450865)应符合 KSPROPERTY返回的数据包计数\_RTAUDIO\_PACKETCOUNT 和驱动程序的数据包编号解释传递到 SetWritePacket。 换而言之，数据包 0 的第一个示例是块 0。

这并不意味着该 KSPROPERTY\_RTAUDIO\_PACKETCOUNT 和 KSPROPERTY\_RTAUDIO\_演示文稿\_位置，如果同时，调用将会返回到相同的示例，请参阅的值。 KSPROPERTY\_RTAUDIO\_PACKETCOUNT 返回信息的示例从 WaveRT 缓冲区传输到的硬件，同时 KSPROPERTY\_RTAUDIO\_演示文稿\_位置返回有关在系统的输出的示例的信息。 这些是信息的两个不同片段。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 10 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

 

 






