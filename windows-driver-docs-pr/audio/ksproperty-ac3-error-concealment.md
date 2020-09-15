---
title: KSPROPERTY \_ E-ac3 \_ 错误 \_ CONCEALMENT
description: KSPROPERTY \_ E-ac3 \_ ERROR \_ CONCEALMENT 属性指定在播放过程中应隐藏 AC 3 编码流中的错误的方式。
ms.assetid: bdf3dd8f-0757-4679-b051-63736503c5b4
keywords:
- KSPROPERTY_AC3_ERROR_CONCEALMENT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_ERROR_CONCEALMENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 449b0bb4b5134713435977bae1d9aa4543c50be8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102340"
---
# <a name="ksproperty_ac3_error_concealment"></a>KSPROPERTY \_ E-ac3 \_ 错误 \_ CONCEALMENT


KSPROPERTY \_ E-ac3 \_ ERROR \_ CONCEALMENT 属性指定在播放过程中应隐藏 AC 3 编码流中的错误的方式。

## <span id="ddk_ksproperty_ac3_error_concealment_ks"></span><span id="DDK_KSPROPERTY_AC3_ERROR_CONCEALMENT_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment" data-raw-source="[&lt;strong&gt;KSAC3_ERROR_CONCEALMENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment)"><strong>KSAC3_ERROR_CONCEALMENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSAC3 \_ 错误 \_ CONCEALMENT 结构，该结构指定如何隐藏包含错误的 AC 3 块。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ E-ac3 \_ 错误 \_ CONCEALMENT 属性请求返回状态 SUCCESS，指示该请求已 \_ 成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSAC3 \_ 错误 \_ CONCEALMENT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment)

