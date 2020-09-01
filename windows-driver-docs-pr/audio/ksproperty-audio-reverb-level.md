---
title: KSPROPERTY \_ 音频 \_ 回音 \_ 电平
description: "\"KSPROPERTY \\_ 音频 \\_ 回音 \\_ 级别\" 属性指定当前 reverberation 级别。 这是回音节点 (KSNODETYPE 回音) 的属性 \\_ 。"
ms.assetid: f38396a2-5528-4085-a051-fcfb73e9c1d1
keywords:
- KSPROPERTY_AUDIO_REVERB_LEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_REVERB_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d46b68e7c349380e95e227c4b98a40d6485ff8c2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208953"
---
# <a name="ksproperty_audio_reverb_level"></a>KSPROPERTY \_ 音频 \_ 回音 \_ 电平


"KSPROPERTY \_ 音频 \_ 回音 \_ 级别" 属性指定当前 reverberation 级别。 这是回音节点 ([**KSNODETYPE \_ 回音**](ksnodetype-reverb.md)) 的属性。

## <span id="ddk_ksproperty_audio_reverb_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_REVERB_LEVEL_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，并指定 reverberation 级别。 回音值后跟0到 100 \* (65536-1/65536) % 之间的线性范围：

-   值0x00010000 表示100%。

-   值0xFFFFFFFF 表示 100 \* (65536-1/65536) %。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 回音 \_ 电平属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSNODETYPE \_ 回音**](ksnodetype-reverb.md)

[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

