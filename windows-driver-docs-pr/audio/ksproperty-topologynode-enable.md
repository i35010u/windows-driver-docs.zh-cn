---
title: KSPROPERTY\_TOPOLOGYNODE\_启用
description: KSPROPERTY\_TOPOLOGYNODE\_启用属性用于启用或禁用的已生成的拓扑中的拓扑节点。
ms.assetid: 6b9f7a92-97dc-476b-962a-40ccf1987154
keywords:
- KSPROPERTY_TOPOLOGYNODE_ENABLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGYNODE_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a59b13d9b73b7d7566b29df7adfc4e1dd88305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555577"
---
# <a name="kspropertytopologynodeenable"></a>KSPROPERTY\_TOPOLOGYNODE\_启用


KSPROPERTY\_TOPOLOGYNODE\_启用属性用于启用或禁用的已生成的拓扑中的拓扑节点。

## <span id="ddk_ksproperty_topologynode_enable_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGYNODE_ENABLE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型 BOOL 的是，它指定该节点打开或关闭。 值为 **，则返回 TRUE**指示节点是否已打开。 **FALSE**指示节点处于关闭状态。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_TOPOLOGYNODE\_启用属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

启用已启用的节点或禁用已禁用的节点没有影响，但不是会视为错误。

禁用节点，将关闭该节点通过节点的流执行的转换。 在 AEC、 AGC 或干扰禁止显示节点的情况下 ([**KSNODETYPE\_声学\_ECHO\_取消**](ksnodetype-acoustic-echo-cancel.md)， [ **KSNODETYPE\_AGC**](ksnodetype-agc.md)，或[ **KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md))，例如，已禁用的节点会在运行直通模式下 （即，它执行任何操作的流从该节点的输入插针流动到其输出插针）。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

[**KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md)

 

 






