---
title: KSPROPERTY\_TOPOLOGYNODE\_重置
description: KSPROPERTY\_TOPOLOGYNODE\_重置属性重置节点完全，将其还原到其初始状态。
ms.assetid: c7558518-53c5-43c6-94ac-107823e2a0ab
keywords:
- KSPROPERTY_TOPOLOGYNODE_RESET 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGYNODE_RESET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6bfdae7ad4e927124cc2b09a034b5f40e4372ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332561"
---
# <a name="kspropertytopologynodereset"></a>KSPROPERTY\_TOPOLOGYNODE\_重置


KSPROPERTY\_TOPOLOGYNODE\_重置属性重置节点完全，将其还原到其初始状态。

## <span id="ddk_ksproperty_topologynode_reset_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGYNODE_RESET_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型布尔值，指示是否应重置节点。 值为 **，则返回 TRUE**将重置节点为其默认的初始状态在创建时。 值为**FALSE**没有影响，但不是会视为错误。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_TOPOLOGYNODE\_重置属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left"><p>Microsoft Windows XP 和更高版本操作系统中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 






