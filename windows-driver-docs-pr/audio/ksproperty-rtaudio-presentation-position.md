---
title: KSPROPERTY \_ RTAUDIO \_ 演示 \_ 位置
description: KSPROPERTY \_ RTAUDIO \_ 演示 \_ 位置返回流演示信息。
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
ms.openlocfilehash: a03d4aef770cd5e2f51cbf62cc68b75fef477727
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210923"
---
# <a name="ksproperty_rtaudio_presentation_position"></a>KSPROPERTY \_ RTAUDIO \_ 演示 \_ 位置


KSPROPERTY \_ RTAUDIO \_ 演示 \_ 位置返回流演示信息。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position"><STRONG>KSAUDIO_PRESENTATION_POSITION</STRONG></a></p></td>
</tr>
</tbody>
</table>
 

属性描述符 (实例数据) 是 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构。 在发送请求之前，客户端会在音频数据流中加载包含描述当前游标位置的值的结构。

属性值是一个 [**KSAUDIO 表示 \_ \_ 位置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position) 结构，它表示音频数据流中最近的演示位置。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ RTAUDIO \_ 演示 \_ 位置属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的失败状态代码。

<a name="remarks"></a>备注
-------

操作系统可能会定期从驱动程序获取此属性，以从驱动程序中检索最近的演示位置信息，以允许上层与音频流同步视频或其他活动。

[**KSAUDIO \_ 表示 \_ 位置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position)的 u64PositionInBlocks 成员中返回的值应与 KSPROPERTY RTAUDIO PACKETCOUNT 返回的数据包计数 \_ \_ 和传递到 SetWritePacket 的数据包编号的驱动程序解释一致。 换句话说，数据包0的第一个示例为块0。

这并不意味着 KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT 和 KSPROPERTY \_ RTAUDIO \_ 呈现 \_ 位置（如果同时调用）将返回引用同一示例的值。 KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT 返回有关从 WaveRT 缓冲区传输到硬件的示例的信息，而 KSPROPERTY \_ RTAUDIO \_ 表示位置将 \_ 返回有关系统输出中提供的示例的信息。 下面是两个不同的信息片段。

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

 

