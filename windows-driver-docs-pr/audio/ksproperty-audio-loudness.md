---
title: KSPROPERTY\_音频\_响度
description: KSPROPERTY\_音频\_响度属性指定是否启用或禁用响度节点中为通道响度 （总体动态范围和低音增强） (KSNODETYPE\_响度)。
ms.assetid: bc567e98-8a04-44f0-9ddf-7b71abf659a5
keywords:
- KSPROPERTY_AUDIO_LOUDNESS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LOUDNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4758984ba4d42f0b40203148b17f41d5f2d28b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333027"
---
# <a name="kspropertyaudioloudness"></a>KSPROPERTY\_音频\_响度


KSPROPERTY\_音频\_响度属性指定是否启用或禁用响度节点中为通道响度 （总体动态范围和低音增强） ([**KSNODETYPE\_响度**](ksnodetype-loudness.md)).

## <span id="ddk_ksproperty_audio_loudness_ks"></span><span id="DDK_KSPROPERTY_AUDIO_LOUDNESS_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型 BOOL 的是，它指定响度打开或关闭。 该值 **，则返回 TRUE**指示是否已启用了响度。 **FALSE**指示它已关闭。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_响度属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSNODETYPE\_响度**](ksnodetype-loudness.md)

 

 






