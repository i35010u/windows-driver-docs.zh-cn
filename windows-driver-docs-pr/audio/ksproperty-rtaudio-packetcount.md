---
title: KSPROPERTY\_RTAUDIO\_PACKETCOUNT
description: KSPROPERTY\_RTAUDIO\_PACKETCOUNT 返回完全从 WaveRT 缓冲区传输到硬件的数据包 （从 1 开始） 计数。
ms.assetid: 904896DE-D135-43B6-AA1F-F49D0748952D
keywords:
- KSPROPERTY_RTAUDIO_PACKETCOUNT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_PACKETCOUNT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 06/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: c726f41ff11389ee6ef7669809f16a52c9783929
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391647"
---
# <a name="kspropertyrtaudiopacketcount"></a>KSPROPERTY\_RTAUDIO\_PACKETCOUNT


KSPROPERTY\_RTAUDIO\_PACKETCOUNT 返回完全从 WaveRT 缓冲区传输到硬件的数据包 （从 1 开始） 计数。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/ulong" data-raw-source="[&lt;strong&gt;ULONG&lt;/strong&gt;](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/ulong)"><strong>ULONG</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 是[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构。 发送请求之前, 在客户端加载的 （从 1 开始） 数量完全从 WaveRT 缓冲区传输到硬件的数据包的结构。

属性值为类型为 ULONG 的变量。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_PACKETCOUNT 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。

<a name="remarks"></a>备注
-------

从数据包计数，操作系统可以派生它将写入到 WaveRT 缓冲区的数据包流的位置。 操作系统也可以派生 WaveRT 缓冲区内编写的下一个数据包的 WaveRT 缓冲区位置。 WaveRT 驱动程序，该驱动程序像它将数据从 WaveRT 缓冲区的每个数据包传输信号单个通知事件。 因此单独的事件不能指示正在传输 WaveRT 缓冲区中的数据包。 在正常操作中这不是关键因素，但在下溢情况下更正更轻松地实现通过查询从该操作系统可以确定接下来编写的数据包的数据包计数。

返回的 PacketCount 指示完全从 WaveRT 缓冲区传输到硬件的数据包 （从 1 开始） 计数。 由此，操作系统可以确定基于 0 的数当前正在被传输的数据包并确保将写入之前该数据包。 例如，如果数据包计数为 5，然后 5 数据包已完全传输。 也就是说，已完全传输数据包 0 到 4。 因此数据包 5 正在进行，并且操作系统应写入数据包 6。 如果 WaveRT 缓冲区的通知计数为 2，则数据包 6 应按 WaveRT 缓冲区中的偏移量 0 （因为减的模 2 6 是 0 和 0 次数据包大小为 0）。

操作系统可能会在任何时候获取此属性。 但是它通常获取此属性只是定期或驱动程序返回数据流错误后 (状态\_数据\_LATE\_错误，状态\_数据\_溢出) 从以便 SetWritePacket()重新同步使用驱动程序。

该驱动程序应将计数重置数据包为 0 时该流位于 KSSTATE\_停止。

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

 

 






