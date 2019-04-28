---
title: KSPROPERTY\_音频\_延迟
description: KSPROPERTY\_音频\_延迟属性用于报告的延迟 （或音频缓冲量） 与流相关联。
ms.assetid: d155e3a5-e3e6-4381-9bbe-2a16b0be47b3
keywords:
- KSPROPERTY_AUDIO_LATENCY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LATENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e171287ffb0ad9a0e1dd3ccb04cadda5c00481
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333025"
---
# <a name="kspropertyaudiolatency"></a>KSPROPERTY\_音频\_延迟


KSPROPERTY\_音频\_延迟属性用于报告的延迟 （或音频缓冲量） 与流相关联。

## <span id="ddk_ksproperty_audio_latency_ks"></span><span id="DDK_KSPROPERTY_AUDIO_LATENCY_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567145" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567145)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为类型指定的流延迟的 KSTIME 的结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_延迟属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于查询 pin AEC 筛选器的流延迟。 有关详细信息，请参阅[Exposing Hardware-Accelerated 捕获效果](https://msdn.microsoft.com/library/windows/hardware/ff536379)。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSTIME**](https://msdn.microsoft.com/library/windows/hardware/ff567145)

 

 






