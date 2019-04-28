---
title: KSPROPERTY\_AUDIO\_MIX\_LEVEL\_CAPS
description: KSPROPERTY\_音频\_混合\_级别\_CAPS 属性指定 supermixer 节点的混合级别功能 (KSNODETYPE\_SUPERMIX)。 单个的 get 属性请求检索的所有组合的输入和输出通道的信息。
ms.assetid: ab7a5dfb-8975-41bb-9347-953406701804
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d88bfa48565a330f244d0c70eaa98fc969418675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332991"
---
# <a name="kspropertyaudiomixlevelcaps"></a>KSPROPERTY\_AUDIO\_MIX\_LEVEL\_CAPS


KSPROPERTY\_音频\_混合\_级别\_CAPS 属性指定 supermixer 节点的混合级别功能 ([**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)). 将单个*获取*-属性请求检索的所有组合的输入和输出通道的信息。

## <span id="ddk_ksproperty_audio_mix_level_caps_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_CAPS_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537088" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXCAP_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537088)"><strong>KSAUDIO_MIXCAP_TABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_MIXCAP\_表，该表指定所有的功能*m*\**n*输入-输出supermixer 节点中的途径*m*输入通道并*n*输出通道。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_混合\_级别\_CAPS 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSAUDIO\_MIXCAP\_TABLE**](https://msdn.microsoft.com/library/windows/hardware/ff537088)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

 

 






