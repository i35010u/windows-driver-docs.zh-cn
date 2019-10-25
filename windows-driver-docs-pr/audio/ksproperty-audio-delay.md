---
title: KSPROPERTY\_音频\_延迟
description: KSPROPERTY\_音频\_延迟属性指示延迟节点（KSNODETYPE\_延迟）引入指定通道的时间延迟。
ms.assetid: ac260b83-1d7c-49d7-b325-ea0f21646d39
keywords:
- KSPROPERTY_AUDIO_DELAY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DELAY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbe571e03dddf41d261407484de98ea9ad353c6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831048"
---
# <a name="ksproperty_audio_delay"></a>KSPROPERTY\_音频\_延迟


KSPROPERTY\_音频\_延迟属性指示延迟节点（[**KSNODETYPE\_延迟**](ksnodetype-delay.md)）引入指定通道的时间延迟。

## <span id="ddk_ksproperty_audio_delay_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DELAY_KS"></span>


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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSTIME 类型的结构，它指定了滞后时间。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_延迟属性请求返回状态\_SUCCESS，指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY\_音频\_频道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSTIME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)

[**KSNODETYPE\_延迟**](ksnodetype-delay.md)

 

 






