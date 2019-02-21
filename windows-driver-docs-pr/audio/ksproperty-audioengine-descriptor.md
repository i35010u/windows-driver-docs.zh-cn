---
title: KSPROPERTY\_AUDIOENGINE\_描述符
description: 卸载支持的硬件解决方案的音频驱动程序使用 KSPROPERTY\_AUDIOENGINE\_描述符提供有关节点表示硬件音频引擎的信息。
ms.assetid: 1D912155-6DB2-4AFF-949F-47C19E47678C
keywords:
- KSPROPERTY_AUDIOENGINE_DESCRIPTOR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_DESCRIPTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 090b206274bad3d6693b5b753163773d6b91db60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527191"
---
# <a name="kspropertyaudioenginedescriptor"></a>KSPROPERTY\_AUDIOENGINE\_描述符


卸载支持的硬件解决方案的音频驱动程序使用**KSPROPERTY\_AUDIOENGINE\_描述符**提供表示硬件音频引擎的节点信息。

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
<td align="left"><p>通过筛选器节点</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh450862" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450862)"><strong>KSAUDIOENGINE_DESCRIPTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值为类型**KSAUDIOENGINE\_描述符**并指示音频引擎节点的静态属性。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOENGINE\_描述符**属性请求将返回**状态\_成功**以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOENGINE\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/hh450862)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






