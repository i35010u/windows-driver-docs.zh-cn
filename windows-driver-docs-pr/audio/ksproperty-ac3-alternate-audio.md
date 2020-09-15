---
title: KSPROPERTY \_ E-ac3 \_ 备用 \_ 音频
description: KSPROPERTY \_ E-ac3 \_ 备用 \_ 音频属性指定是否应将 AC 3 编码流中的两个 mono 通道解释为立体声对或两个独立的程序通道。
ms.assetid: fff2c52f-c996-4dfe-a46e-9f937cbd0d8c
keywords:
- KSPROPERTY_AC3_ALTERNATE_AUDIO 音频设备
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
ms.openlocfilehash: fbadccad6618c816293f0b48c294274cf1fac603
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102356"
---
# <a name="ksproperty_ac3_alternate_audio"></a>KSPROPERTY \_ E-ac3 \_ 备用 \_ 音频


KSPROPERTY \_ E-ac3 \_ 备用 \_ 音频属性指定是否应将 AC 3 编码流中的两个 mono 通道解释为立体声对或两个独立的程序通道。

## <span id="ddk_ksproperty_ac3_alternate_audio_ks"></span><span id="DDK_KSPROPERTY_AC3_ALTERNATE_AUDIO_KS"></span>


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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_alternate_audio" data-raw-source="[&lt;strong&gt;KSAC3_ALTERNATE_AUDIO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_alternate_audio)"><strong>KSAC3_ALTERNATE_AUDIO</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSAC3 \_ 备用 \_ 音频结构，用于指定应如何解释两个 mono 通道。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ E-ac3 \_ 备用 \_ 音频属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSAC3 \_ 备用 \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_alternate_audio)

