---
title: KSPROPERTY\_RTAUDIO\_HWLATENCY
description: KSPROPERTY\_RTAUDIO\_HWLATENCY 属性检索的音频硬件和其关联的数据路径的流延迟的说明。 下表总结了此属性的功能。
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
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94cc647ea4756d1a8607a469b125847e24d6433e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332671"
---
# <a name="kspropertyrtaudiohwlatency"></a>KSPROPERTY\_RTAUDIO\_HWLATENCY


KSPROPERTY\_RTAUDIO\_HWLATENCY 属性检索的音频硬件和其关联的数据路径的流延迟的说明。

下表总结了此属性的功能。

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
<td align="left"><p><a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwlatency"><strong>KSRTAUDIO_HWLATENCY</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_HWLATENCY 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。

<a name="remarks"></a>备注
-------

之后[WaveRT 微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538845)已经分配了循环缓冲区 (请参阅[ **KSPROPERTY\_RTAUDIO\_缓冲区**](ksproperty-rtaudio-buffer.md)) 客户端可以发送KSPROPERTY\_RTAUDIO\_HWLATENCY 属性请求对驱动程序硬件延迟的信息。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSRTAUDIO\_HWLATENCY**](https://msdn.microsoft.com/library/windows/hardware/ff537496)

[**KSPROPERTY\_RTAUDIO\_缓冲区**](ksproperty-rtaudio-buffer.md)

[WaveRT 微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538845)

 

 






