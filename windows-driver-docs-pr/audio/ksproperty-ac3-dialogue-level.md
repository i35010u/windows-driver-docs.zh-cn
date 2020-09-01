---
title: KSPROPERTY \_ E-ac3 \_ 对话框 \_ 级别
description: KSPROPERTY \_ E-ac3 \_ 对话框 \_ LEVEL 属性指定 AC 3 编码流中音频程序内的口述对话的平均音量级别。
ms.assetid: 8b88b631-abf7-4407-a7c1-ddacf849a81e
keywords:
- KSPROPERTY_AC3_DIALOGUE_LEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_DIALOGUE_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00c4da745818d874174781a558952bb75691986c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209023"
---
# <a name="ksproperty_ac3_dialogue_level"></a>KSPROPERTY \_ E-ac3 \_ 对话框 \_ 级别


KSPROPERTY \_ E-ac3 \_ 对话框 \_ LEVEL 属性指定 AC 3 编码流中音频程序内的口述对话的平均音量级别。

## <span id="ddk_ksproperty_ac3_dialogue_level_ks"></span><span id="DDK_KSPROPERTY_AC3_DIALOGUE_LEVEL_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_dialogue_level" data-raw-source="[&lt;strong&gt;KSAC3_DIALOGUE_LEVEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_dialogue_level)"><strong>KSAC3_DIALOGUE_LEVEL</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 \_ \_ 指定平均对话框级别的 KSAC3 对话框级结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ E-ac3 \_ 对话 \_ LEVEL 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSAC3 \_ 对话框 \_ 级别**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_dialogue_level)

 

