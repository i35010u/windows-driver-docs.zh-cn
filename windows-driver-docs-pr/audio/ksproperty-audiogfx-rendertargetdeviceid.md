---
title: KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID
description: KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID 属性用来通知 GFX 筛选器的呈现最终音频混合的音频设备的即插设备 ID。
ms.assetid: 66251f22-a2e3-453e-985a-74ff18a60e66
keywords:
- KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 552c112480acb840cccafb8f1d38bfa9baa8187b
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391455"
---
# <a name="kspropertyaudiogfxrendertargetdeviceid"></a>KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID


KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID 属性用来通知 GFX 筛选器的呈现最终音频混合的音频设备的即插设备 ID。

## <span id="ddk_ksproperty_audiogfx_rendertargetdeviceid_ks"></span><span id="DDK_KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>WCHAR 数组</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 WCHAR 数组，其中包含设备 id。 设备 ID 是以 null 结尾的 Unicode 字符的字符串。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此设置只读属性，请求的目标是 GFX 筛选器配置用作是呈现 / 捕获 GFX 筛选器。

若要确定保存属性值所需的缓冲区的大小，请参阅[音频属性的基本支持查询](https://docs.microsoft.com/windows-hardware/drivers/audio/basic-support-queries-for-audio-properties)。

有关设备 Id 的其他信息，请参阅[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






