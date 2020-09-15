---
title: KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT
description: KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT 返回从 WaveRT 缓冲区完全传输到硬件的) 基于 (1 的数据包数。
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
ms.openlocfilehash: b3253d308bba8d733ad7b43c8a74e9467cc75dd4
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101946"
---
# <a name="ksproperty_rtaudio_packetcount"></a>KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT


KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT 返回从 WaveRT 缓冲区完全传输到硬件的) 基于 (1 的数据包数。

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
<td align="left"><p><a href="/dotnet/csharp/language-reference/keywords/ulong" data-raw-source="[&lt;strong&gt;ULONG&lt;/strong&gt;](/dotnet/csharp/language-reference/keywords/ulong)"><strong>ULONG</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 是 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构。 在发送请求之前，客户端会将结构 (与从 WaveRT 缓冲区完全传输的数据包的) 计数转换为硬件。

属性值是 ULONG 类型的变量。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的失败状态代码。

<a name="remarks"></a>注解
-------

从数据包计数中，OS 可以派生出其写入到 WaveRT 缓冲区的数据包的流位置。 操作系统还可以派生下一个数据包的 WaveRT 缓冲区位置，以便在 WaveRT 缓冲区中写入。 对于 WaveRT 驱动程序，驱动程序会发出单个通知事件的信号，因为它会从每个 WaveRT 缓冲区包中传输数据。 因此，单独的事件无法指示正在传输 WaveRT 缓冲区中的数据包。 在正常操作中，这并不是问题，但在下溢情况下，通过查询 OS 可以确定要写入的数据包的数据包计数，可以更轻松地实现更正。

返回的 PacketCount 指示从 WaveRT 缓冲区完全传输到硬件的数据包 (1 的) 计数。 从此，操作系统可以确定当前正在传输的数据包的从0开始的数目，并确保它在该数据包之前写入。 例如，如果数据包计数为5，则5个数据包已完全传输。 也就是说，包0-4 已完全传输。 因此，数据包5正在进行，操作系统应该写入数据包6。 如果 WaveRT 缓冲区的通知计数为2，则数据包6将为 WaveRT (缓冲区中的偏移量0，因为6模2为0，数据包大小为0次) 。

操作系统可以随时获取此属性。 不过，通常情况下，它只会定期或在驱动程序返回数据流错误之后 (状态 \_ 数据 \_ \_ "延迟" 错误、 \_ \_ 从 SetWritePacket ( # A3 状态数据溢出) 以便与驱动程序重新同步。

当流处于 KSSTATE 停止时，驱动程序应将数据包计数重置为 0 \_ 。

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
<td align="left"><p>适用于 Windows 10 及更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID \_ RTAudio](kspropsetid-rtaudio.md)

