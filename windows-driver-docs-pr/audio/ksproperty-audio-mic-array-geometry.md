---
title: KSPROPERTY\_音频\_MIC\_数组\_几何图形
description: KSPROPERTY\_音频\_MIC\_array\_GEOMETRY 属性指定麦克风阵列的几何。
ms.assetid: c9153c65-06d1-4968-8d70-64aafc760a8c
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
ms.openlocfilehash: bcfc821fa11245addbae124bb2f289a95366afd6
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925592"
---
# <a name="ksproperty_audio_mic_array_geometry"></a>KSPROPERTY\_音频\_MIC\_数组\_几何图形


KSPROPERTY\_音频\_MIC\_array\_GEOMETRY 属性指定麦克风阵列的几何。

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
<td align="left"><p>Get</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>属性描述符类型</p></td>
<td align="left"><p>属性值类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry" data-raw-source="[&lt;strong&gt;KSAUDIO_MIC_ARRAY_GEOMETRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)"><strong>KSAUDIO_MIC_ARRAY_GEOMETRY</strong></a></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 KSAUDIO\_MIC\_ARRAY\_GEOMETRY。 有关详细信息，请[**参阅\_KSAUDIO\_MIC\_ARRAY GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)结构的定义。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

当请求\_成功\_完成\_后\_，KSPROPERTY 音频 MIC ARRAY GEOMETRY\_属性请求返回状态成功。

如果[**KSP\_Pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)结构的 PinId 成员指示的 pin 不支持 mic 数组请求，则该属性请求将返回不\_受支持的状态\_。

如果请求的缓冲区大小设置为零，则属性请求将返回状态\_缓冲区\_溢出状态。 此外，请求将使用返回状态块指示 pin 支持的 KSAUDIO\_MIC\_数组\_几何结构的大小。

如果请求的缓冲区大小设置为太小而不能容纳返回的结构，则请求返回的状态\_缓冲区\_太\_小。 然后，该请求将使用返回状态块指示 pin 支持的[**KSAUDIO\_\_MIC 数组\_几何**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)结构的大小。

<a name="remarks"></a>备注
-------

KSPROPERTY\_音频\_MIC\_ARRAY\_GEOMETRY 属性仅支持 KSPROPERTY\_类型\_GET 请求。 为了使客户端能够确定要容纳整个 geometry 结构所需的缓冲区的正确大小，必须首先使该请求的缓冲区大小为零。 然后，客户端可以使用状态块中返回的值正确设置缓冲区大小，然后再使用正确大小的缓冲区进行另一个属性请求。

有关如何在 Windows 中处理麦克风阵列的详细信息，请参阅以下资源：

[麦克风阵列几何属性](https://docs.microsoft.com/windows-hardware/drivers/audio/microphone-array-geometry-property)

[Windows 中的麦克风阵列支持（白皮书）](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613960(v=vs.85))

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIO\_MIC\_数组\_几何图形**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






