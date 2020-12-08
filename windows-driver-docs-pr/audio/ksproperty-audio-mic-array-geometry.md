---
title: KSPROPERTY \_ 音频 \_ MIC \_ 数组 \_ 几何图形
description: KSPROPERTY \_ 音频 \_ MIC \_ array \_ GEOMETRY 属性指定麦克风阵列的几何。
keywords:
- KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9579e93cfa29d3b7bc2e0a01d629ae8cd4082d8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784511"
---
# <a name="ksproperty_audio_mic_array_geometry"></a>KSPROPERTY \_ 音频 \_ MIC \_ 数组 \_ 几何图形


KSPROPERTY \_ 音频 \_ MIC \_ array \_ GEOMETRY 属性指定麦克风阵列的几何。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>获取</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>属性描述符类型</p></td>
<td align="left"><p>属性值类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry" data-raw-source="[&lt;strong&gt;KSAUDIO_MIC_ARRAY_GEOMETRY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)"><strong>KSAUDIO_MIC_ARRAY_GEOMETRY</strong></a></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (类型为 KSAUDIO \_ MIC \_ ARRAY \_ GEOMETRY。 有关详细信息，请参阅 [**KSAUDIO \_ MIC \_ ARRAY \_ GEOMETRY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry) 结构的定义。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_ \_ \_ 当请求成功完成后，KSPROPERTY 音频 MIC ARRAY \_ GEOMETRY 属性请求返回状态 \_ 成功。

如果 [**KSP \_ pin**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) 结构的 PinId 成员指示的 pin 不支持 mic 数组请求，则该属性请求将返回 \_ 不 \_ 受支持的状态。

如果请求的缓冲区大小设置为零，则属性请求将返回状态 \_ 缓冲区 \_ 溢出状态。 此外，请求将使用返回状态块指示 \_ pin 支持的 KSAUDIO MIC \_ 数组几何结构的大小 \_ 。

如果请求的缓冲区大小设置为太小而不能容纳返回的结构，则请求返回的状态 \_ 缓冲区 \_ 太 \_ 小。 然后，该请求将使用返回状态块指示 pin 支持的 [**KSAUDIO \_ MIC \_ 数组 \_ 几何**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry) 结构的大小。

<a name="remarks"></a>备注
-------

KSPROPERTY \_ 音频 \_ MIC \_ ARRAY \_ GEOMETRY 属性仅支持 KSPROPERTY \_ 类型 \_ GET 请求。 为了使客户端能够确定要容纳整个 geometry 结构所需的缓冲区的正确大小，必须首先使该请求的缓冲区大小为零。 然后，客户端可以使用状态块中返回的值正确设置缓冲区大小，然后再使用正确大小的缓冲区进行另一个属性请求。

有关如何在 Windows 中处理麦克风阵列的详细信息，请参阅以下资源：

[麦克风阵列几何属性](./microphone-array-geometry-property.md)

[Windows (白皮书中的麦克风阵列支持) ](/previous-versions/windows/hardware/design/dn613960(v=vs.85))

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIO \_ MIC \_ 数组 \_ 几何图形**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

