---
title: KSPROPERTY\_AUDIOENGINE\_LOOPBACK\_PROTECTION
description: KSPROPERTY\_AUDIOENGINE\_环回\_保护属性请求将允许音频驱动程序设置的音频引擎节点的环回保护状态。
ms.assetid: E798582C-7662-413C-B25C-6A129FDEEE38
keywords:
- KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de57599601cfbb434ab859330d2ab0c587b88a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563575"
---
# <a name="kspropertyaudioengineloopbackprotection"></a>KSPROPERTY\_AUDIOENGINE\_LOOPBACK\_PROTECTION


**KSPROPERTY\_AUDIOENGINE\_环回\_保护**属性请求将允许音频驱动程序设置的音频引擎节点的环回保护状态。

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
<td align="left"><p>通过 Pin 实例的节点</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AUDIOENGINE\_环回\_保护属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

与此属性调用相关联的输入的缓冲区填充与枚举值的类型 CONSTRICTOR\_选项。 因此输入的缓冲区被设置为 CONSTRICTOR\_选项\_禁用或 CONSTRICTOR\_选项\_静音。

如果有任何活动流与 CONSTRICTOR\_选项\_静音有效，则此音频输出 KS 环回点击就会发出静默。 如果所有活动流有 CONSTRICTOR\_选项\_，只有禁用起作用 （这是默认状态），然后将环回分流点是否包含有意义的数据。

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

 

 






