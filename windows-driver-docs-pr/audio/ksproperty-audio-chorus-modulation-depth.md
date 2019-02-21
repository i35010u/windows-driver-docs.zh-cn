---
title: KSPROPERTY\_音频\_合唱团\_调制\_深度
description: KSPROPERTY\_音频\_合唱团\_调制\_DEPTH 属性指定合唱团调制深度。 这是合唱团节点的属性 (KSNODETYPE\_合唱团)。
ms.assetid: A14DA707-7ED6-4E86-87C7-9A4E40062FE8
keywords:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_DEPTH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59517963e67bb31a94db8267cf1c7578826f2bb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520367"
---
# <a name="kspropertyaudiochorusmodulationdepth"></a>KSPROPERTY\_音频\_合唱团\_调制\_深度


KSPROPERTY\_音频\_合唱团\_调制\_DEPTH 属性指定合唱团调制深度。 这是合唱团节点的属性 ([**KSNODETYPE\_合唱团**](ksnodetype-chorus.md))。

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
<td align="left"><p>KSNODEPROPERTY</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值为类型为 ULONG，它指定合唱团调制深度。 它表示以毫秒为单位，并设置调制器的速度 （频率）。 值可以介于 0 和 1/256th 增量 255.9961。 若要解决此问题，属性值应表示为定点 16.16 值，满足以下条件：

-   值 0x00010000 表示 1 毫秒
-   值为 0xFFFFFFFF 表示 (65536 的 1/65536) ms

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_合唱团\_调制\_深度属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_合唱团**](ksnodetype-chorus.md)

 

 






