---
title: KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY
description: KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY 属性指定几何图形的麦克风阵列。
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
ms.openlocfilehash: 129d60dc933d6053dad78ebfab2507af408e0edb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333031"
---
# <a name="kspropertyaudiomicarraygeometry"></a>KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY


KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY 属性指定几何图形的麦克风阵列。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

使用率摘要表

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
<td align="left"><p>Filter</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537087" data-raw-source="[&lt;strong&gt;KSAUDIO_MIC_ARRAY_GEOMETRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537087)"><strong>KSAUDIO_MIC_ARRAY_GEOMETRY</strong></a></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 KSAUDIO\_MIC\_数组\_几何图形。 请参阅的定义[ **KSAUDIO\_MIC\_数组\_GEOMETRY** ](https://msdn.microsoft.com/library/windows/hardware/ff537087)结构有关的详细信息。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY 属性请求返回状态\_请求的成功完成后成功。

如果 pin 由 PinId 隶属[ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)结构不支持的 mic 数组请求，则属性请求将返回状态\_不\_受支持。

如果请求的缓冲区大小设置为零，则属性请求将返回状态\_缓冲区\_溢出状态。 此外，请求将使用返回状态块来指示大小 KSAUDIO\_MIC\_数组\_受 pin 的几何结构。

如果请求的缓冲区大小设置为任何缓冲区大小太小，无法容纳返回的结构，该请求返回的状态\_缓冲区\_过\_小。 请求然后将使用返回状态块来指示的大小[ **KSAUDIO\_MIC\_数组\_GEOMETRY** ](https://msdn.microsoft.com/library/windows/hardware/ff537087)受 pin 的结构。

<a name="remarks"></a>备注
-------

KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY 属性仅支持 KSPROPERTY\_类型\_GET 请求。 为了使客户端确定正确容纳整个几何结构所需的缓冲区的大小，它必须先将缓冲区大小为零的请求。 客户端可以然后使用返回状态块中的值正确设置缓冲区大小，然后进行正确大小的缓冲区与另一个属性请求。

有关如何处理 Windows 上的麦克风阵列的详细信息，请参阅以下资源：

[在 Windows （白皮书） 中的麦克风阵列支持](https://go.microsoft.com/fwlink/p/?linkid=120592)

[麦克风阵列 Geometry 属性](https://msdn.microsoft.com/library/windows/hardware/ff537516.aspx)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIO\_MIC\_ARRAY\_GEOMETRY**](https://msdn.microsoft.com/library/windows/hardware/ff537087)

[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

 

 






