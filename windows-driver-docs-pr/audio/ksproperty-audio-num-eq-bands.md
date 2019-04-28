---
title: KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS
description: KSPROPERTY\_音频\_NUM\_EQ\_带区属性用于检索频率均衡表中的带区的数目。 这是通道 EQ 节点中的一个只读属性 (KSNODETYPE\_均衡器)。
ms.assetid: b7bb9f05-0b27-4b41-aa38-efb87fc1beee
keywords:
- KSPROPERTY_AUDIO_NUM_EQ_BANDS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_NUM_EQ_BANDS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f67ba732e22f69e63155a406330ea03e5149a3b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332965"
---
# <a name="kspropertyaudionumeqbands"></a>KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS


KSPROPERTY\_音频\_NUM\_EQ\_带区属性用于检索频率均衡表中的带区的数目。 这是通道 EQ 节点中的一个只读属性 ([**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md))。

## <span id="ddk_ksproperty_audio_num_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_NUM_EQ_BANDS_KS"></span>


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
<td align="left"><p>Filter</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，节点的均衡表中指定的频率带区数。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_NUM\_EQ\_带区属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

结合使用此属性[ **KSPROPERTY\_音频\_EQ\_带区**](ksproperty-audio-eq-bands.md)并[ **KSPROPERTY\_音频\_EQ\_级别**](ksproperty-audio-eq-level.md)属性以确定包含这些属性的值是数组的长度。

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

 

 






