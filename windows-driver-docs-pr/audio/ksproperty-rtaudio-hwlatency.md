---
title: KSPROPERTY\_RTAUDIO\_HWLATENCY
description: KSPROPERTY\_RTAUDIO\_HWLATENCY 属性检索音频硬件的流延迟及其关联数据路径的说明。 下表汇总了此属性的功能。
ms.assetid: 5083f281-853a-464e-95d3-0fe14fe00c1c
keywords:
- KSPROPERTY_RTAUDIO_HWLATENCY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_HWLATENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6b6717f37170aa261837734a44b0f43b1338c61a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830682"
---
# <a name="ksproperty_rtaudio_hwlatency"></a>KSPROPERTY\_RTAUDIO\_HWLATENCY


KSPROPERTY\_RTAUDIO\_HWLATENCY 属性检索音频硬件的流延迟及其关联数据路径的说明。

下表汇总了此属性的功能。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwlatency"><strong>KSRTAUDIO_HWLATENCY</strong></a></p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_HWLATENCY 属性请求返回状态\_SUCCESS，以指示该请求已成功完成。 否则，请求将返回相应的失败状态代码。

<a name="remarks"></a>备注
-------

[WaveRT 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/wavert-miniport-driver)分配了循环缓冲区后（请参阅[**KSPROPERTY\_RTAUDIO\_buffer**](ksproperty-rtaudio-buffer.md)），客户端可以向驱动程序发送 KSPROPERTY\_RTAUDIO\_HWLATENCY 属性请求，以获取硬件延迟信息.

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO\_HWLATENCY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwlatency)

[**KSPROPERTY\_RTAUDIO\_缓冲区**](ksproperty-rtaudio-buffer.md)

[**WaveRT 微型端口驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/audio/wavert-miniport-driver)
