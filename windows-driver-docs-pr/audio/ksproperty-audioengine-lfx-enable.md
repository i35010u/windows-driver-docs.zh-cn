---
title: KSPROPERTY\_AUDIOENGINE\_LFXENABLE
description: KSPROPERTY\_AUDIOENGINE\_LFXENABLE 属性请求检索或更改音频引擎节点，有关其处理能力的本地效果的状态。
ms.assetid: 60ACA467-6C70-46EE-B307-06CEE140A0AF
keywords:
- KSPROPERTY_AUDIOENGINE_LFXENABLE Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_LFXENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdaaa30a4937fe8490c792fdd5d0bc7c0aecf7a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575504"
---
# <a name="kspropertyaudioenginelfxenable"></a>KSPROPERTY\_AUDIOENGINE\_LFXENABLE


**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**属性请求检索或更改音频引擎节点，有关其处理能力的本地效果的状态。

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
<td align="left"><p>通过 Pin 实例的节点</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值为类型**BOOL**和指示是否启用对指定的流处理的本地效果。 值为 **，则返回 TRUE**指示处理已启用。 **FALSE**指示已禁用。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**属性请求将返回**状态\_成功**以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**](ksproperty-audioengine-gfx-enable.md)

 

 






