---
title: KSPROPERTY\_AEC\_NOISE\_FILL\_ENABLE
description: KSPROPERTY\_AEC\_干扰\_填充\_启用属性用于启用和禁用背景噪音填充。 此为可选属性的 AEC 节点 (KSNODETYPE\_声学\_ECHO\_取消)。
ms.assetid: 7c0ed4ba-d25e-42b5-b213-fbe74040a453
keywords:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d74467c27f11af5657f5f3f6e4cdbb112f4197ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576705"
---
# <a name="kspropertyaecnoisefillenable"></a>KSPROPERTY\_AEC\_NOISE\_FILL\_ENABLE


KSPROPERTY\_AEC\_干扰\_填充\_启用属性用于启用和禁用背景噪音填充。 此为可选的 AEC 节点的属性 ([**KSNODETYPE\_声学\_ECHO\_取消**](ksnodetype-acoustic-echo-cancel.md))。

## <span id="ddk_ksproperty_aec_noise_fill_enable_ks"></span><span id="DDK_KSPROPERTY_AEC_NOISE_FILL_ENABLE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为类型 BOOL。 此值设置为 **，则返回 TRUE**使能够后台干扰填充。 启用时，节点插入到捕获流背景噪音。 此值设置为**FALSE**禁用后台干扰填充。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AEC\_干扰\_填充\_启用属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

AEC 节点插入背景舒适噪音捕获流中以避免发生时捕获的数据流设置为零，完美 echo 取消后不自然静默。

当创建筛选器包含 AEC 节点或节点重置时，默认情况下禁用背景噪音填充。

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

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

 

 






