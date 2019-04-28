---
title: KSPROPERTY\_AC3\_错误\_隐蔽
description: KSPROPERTY\_AC3\_错误\_隐蔽属性指定在播放期间应在其中隐藏 AC-3 编码流中的错误的方式。
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
ms.openlocfilehash: 3af395773d634551d0d836279fa955972ac7e832
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333136"
---
# <a name="kspropertyac3errorconcealment"></a>KSPROPERTY\_AC3\_错误\_隐蔽


KSPROPERTY\_AC3\_错误\_隐蔽属性指定在播放期间应在其中隐藏 AC-3 编码流中的错误的方式。

## <span id="ddk_ksproperty_ac3_error_concealment_ks"></span><span id="DDK_KSPROPERTY_AC3_ERROR_CONCEALMENT_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537080" data-raw-source="[&lt;strong&gt;KSAC3_ERROR_CONCEALMENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537080)"><strong>KSAC3_ERROR_CONCEALMENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSAC3\_错误\_隐蔽结构，它指定应如何隐藏 ac-3 块包含错误。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AC3\_错误\_隐蔽属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAC3\_错误\_隐蔽**](https://msdn.microsoft.com/library/windows/hardware/ff537080)

 

 






