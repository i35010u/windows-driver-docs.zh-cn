---
title: KSPROPERTY\_AC3\_ALTERNATE\_AUDIO
description: KSPROPERTY\_AC3\_备用\_音频属性指定的 AC-3 编码流中的两个 mono 通道应解释为立体声对还是两个独立的程序通道。
ms.assetid: fff2c52f-c996-4dfe-a46e-9f937cbd0d8c
keywords:
- KSPROPERTY_AC3_ALTERNATE_AUDIO Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_ALTERNATE_AUDIO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5caa97575d6b385bb45e33359088e76a274a3eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525479"
---
# <a name="kspropertyac3alternateaudio"></a>KSPROPERTY\_AC3\_ALTERNATE\_AUDIO


KSPROPERTY\_AC3\_备用\_音频属性指定的 AC-3 编码流中的两个 mono 通道应解释为立体声对还是两个独立的程序通道。

## <span id="ddk_ksproperty_ac3_alternate_audio_ks"></span><span id="DDK_KSPROPERTY_AC3_ALTERNATE_AUDIO_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537055" data-raw-source="[&lt;strong&gt;KSAC3_ALTERNATE_AUDIO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537055)"><strong>KSAC3_ALTERNATE_AUDIO</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSAC3\_备用\_音频结构，它指定应如何解释 mono 的两个通道。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AC3\_备用\_音频属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAC3\_ALTERNATE\_AUDIO**](https://msdn.microsoft.com/library/windows/hardware/ff537055)

 

 






