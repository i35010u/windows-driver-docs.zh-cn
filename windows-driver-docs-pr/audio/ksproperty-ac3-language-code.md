---
title: KSPROPERTY\_AC3\_LANGUAGE\_CODE
description: KSPROPERTY\_AC3\_语言\_代码属性指定的语言代码的 AC-3 编码流。
ms.assetid: 42c0fb44-437c-4fa9-95ee-823880028369
keywords:
- KSPROPERTY_AC3_LANGUAGE_CODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_LANGUAGE_CODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2922b44d5bb6a6cea8a8aa3e55aa0fed015403d8
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391492"
---
# <a name="kspropertyac3languagecode"></a>KSPROPERTY\_AC3\_LANGUAGE\_CODE


KSPROPERTY\_AC3\_语言\_代码属性指定的语言代码的 AC-3 编码流。

## <span id="ddk_ksproperty_ac3_language_code_ks"></span><span id="DDK_KSPROPERTY_AC3_LANGUAGE_CODE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537081(v=vs.85)" data-raw-source="[&lt;strong&gt;KSAC3_LANGUAGE_CODE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537081(v=vs.85))"><strong>KSAC3_LANGUAGE_CODE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSAC3\_语言\_代码结构，它指定的语言代码。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AC3\_语言\_代码属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAC3\_语言\_代码**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537081(v=vs.85))

 

 






