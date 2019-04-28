---
title: KSPROPERTY\_AC3\_BIT\_STREAM\_MODE
description: KSPROPERTY\_AC3\_位\_流\_模式属性指定的位流模式，它是到 ac-3 流编码的音频服务的类型。
ms.assetid: ee3705f5-f16d-4f5e-a551-bea8986d88b6
keywords:
- KSPROPERTY_AC3_BIT_STREAM_MODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_BIT_STREAM_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e887c9b82236e74b6de8de98fd6a215979eb87f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333158"
---
# <a name="kspropertyac3bitstreammode"></a>KSPROPERTY\_AC3\_BIT\_STREAM\_MODE


KSPROPERTY\_AC3\_位\_流\_模式属性指定的位流模式，它是到 ac-3 流编码的音频服务的类型。

## <span id="ddk_ksproperty_ac3_bit_stream_mode_ks"></span><span id="DDK_KSPROPERTY_AC3_BIT_STREAM_MODE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537077" data-raw-source="[&lt;strong&gt;KSAC3_BIT_STREAM_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537077)"><strong>KSAC3_BIT_STREAM_MODE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSAC3\_位\_流\_模式结构，它指定的位流模式。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AC3\_位\_流\_模式属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSAC3\_BIT\_STREAM\_MODE**](https://msdn.microsoft.com/library/windows/hardware/ff537077)

 

 






