---
title: KSPROPERTY\_音频\_混合\_级别\_CAP
description: KSPROPERTY\_音频\_混合\_级别\_CAP 属性指定 supermixer 节点的混合级别功能（KSNODETYPE\_SUPERMIX）。 单个 get 属性请求检索输入和输出通道的所有组合的信息。
ms.assetid: ab7a5dfb-8975-41bb-9347-953406701804
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a93904ae67b79c7196806ae2e67170059abc4394
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831016"
---
# <a name="ksproperty_audio_mix_level_caps"></a>KSPROPERTY\_音频\_混合\_级别\_CAP


KSPROPERTY\_音频\_混合\_级别\_CAP 属性指定 supermixer 节点的混合级别功能（[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)）。 单个*get*属性请求检索输入和输出通道的所有组合的信息。

## <span id="ddk_ksproperty_audio_mix_level_caps_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_CAPS_KS"></span>


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
<td align="left"><p>无</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXCAP_TABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)"><strong>KSAUDIO_MIXCAP_TABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSAUDIO\_\_MIXCAP 类型的结构，它指定 supermixer 节点中所有*m*\**n*输入输出路径的功能，其中包含*m*输入通道和*n*输出通道。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_混合\_级别\_CAP 属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSAUDIO\_MIXCAP\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

 

 






