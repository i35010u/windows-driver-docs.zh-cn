---
title: KSPROPERTY\_音频\_合唱团\_调制\_速率
description: KSPROPERTY\_音频\_合唱团\_调制\_速率属性指定合唱团调制速率。 这是合唱团节点的属性 (KSNODETYPE\_合唱团)。
ms.assetid: 5B57D4C9-E5D1-4407-9556-D59D11DAB1AB
keywords:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_MODULATION_RATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b37cbcb793bc409783a28e6fae174e196e8c1a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333100"
---
# <a name="kspropertyaudiochorusmodulationrate"></a>KSPROPERTY\_音频\_合唱团\_调制\_速率


KSPROPERTY\_音频\_合唱团\_调制\_速率属性指定合唱团调制速率。 这是合唱团节点的属性 ([**KSNODETYPE\_合唱团**](ksnodetype-chorus.md))。

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

 

属性的值为类型为 ULONG，并指定合唱团调制速率。 它以 Hz。 值可以介于 0 和 1/256th 增量 255.9961。 若要解决此问题，属性值应表示为定点 16.16 值，满足以下条件：

-   值 0x00010000 表示 1 Hz
-   值 0xFFFFFFFF 表示 (65536 的 1/65536) Hz

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_合唱团\_调制\_速率属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_合唱团**](ksnodetype-chorus.md)

 

 






