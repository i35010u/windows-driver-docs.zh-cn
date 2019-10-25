---
title: KSPROPERTY\_音频\_低音\_提高
description: KSPROPERTY\_音频\_低音\_提升属性启用和禁用低音节点中通道的低音提升（KSNODETYPE\_声调）。
ms.assetid: aa54b88b-e251-4d16-9ced-842fec569914
keywords:
- KSPROPERTY_AUDIO_BASS_BOOST 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BASS_BOOST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925cdbb2481eb6c4366b5a942ba671f6686f47f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833048"
---
# <a name="ksproperty_audio_bass_boost"></a>KSPROPERTY\_音频\_低音\_提高


KSPROPERTY\_音频\_低音\_提升属性启用和禁用低音节点中通道的低音提升（[**KSNODETYPE\_声调**](ksnodetype-tone.md)）。

## <span id="ddk_ksproperty_audio_bass_boost_ks"></span><span id="DDK_KSPROPERTY_AUDIO_BASS_BOOST_KS"></span>


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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 BOOL，指示是否打开或关闭低音提升。 如果值为**TRUE** ，则表示为指定的通道启用低音提升。 **FALSE**指示它已关闭。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_低音\_提升属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

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

 

 






