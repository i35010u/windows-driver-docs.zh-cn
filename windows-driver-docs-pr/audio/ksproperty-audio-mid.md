---
title: KSPROPERTY\_音频\_MID
description: KSPROPERTY\_音频\_MID 属性指定声调节点中通道的中间频率级别（KSNODETYPE\_声调）。
ms.assetid: cb2555d4-5224-42a6-b364-70de91a44924
keywords:
- KSPROPERTY_AUDIO_MID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ced9889c6fd82adbc76310f4820e13407550bd6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832980"
---
# <a name="ksproperty_audio_mid"></a>KSPROPERTY\_音频\_MID


KSPROPERTY\_音频\_MID 属性指定声调节点中通道的中间频率级别（[**KSNODETYPE\_声调**](ksnodetype-tone.md)）。

## <span id="ddk_ksproperty_audio_mid_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MID_KS"></span>


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
<td align="left"><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 LONG，并指定中间频率级别。 级别值使用以下比例：

-2147483648 为-无限大分贝（衰减），

-2147483647 为-32767.99998474 分贝（衰减），并且

\+ 2147483647 为 + 32767.99998474 分贝（增益）。

由整数值（2147483648到 + 2147483647）表示的分贝范围，其中

此刻度的分辨率为1/65536 分贝。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MID 属性请求返回状态\_SUCCESS，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

筛选器将成功 KSPROPERTY\_音频\_MID 集属性请求，该请求指定超出筛选范围的值，但会将该值固定到支持的范围。 但在后续请求中，此属性将输出所使用的实际值。

声调节点可以支持用于控制高音级别、中端级别、低音级别和低音增强的属性。 有关详细信息，请参阅[**KSNODETYPE\_声调**](ksnodetype-tone.md)。

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

[**KSNODETYPE\_音**](ksnodetype-tone.md)

 

 






