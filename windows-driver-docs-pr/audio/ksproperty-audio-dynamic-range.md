---
title: KSPROPERTY\_音频\_动态\_范围
description: KSPROPERTY\_音频\_动态\_范围属性指定从响度节点（KSNODETYPE\_响度）输出的音频流的动态范围。
ms.assetid: bab1cc2c-0751-4425-8546-9587baece585
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2a26ac744347cf45965702bcf00509c97752e56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831041"
---
# <a name="ksproperty_audio_dynamic_range"></a>KSPROPERTY\_音频\_动态\_范围


KSPROPERTY\_音频\_动态\_范围属性指定从响度节点（[**KSNODETYPE\_响度**](ksnodetype-loudness.md)）输出的音频流的动态范围。

## <span id="ddk_ksproperty_audio_dynamic_range_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_RANGE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range" data-raw-source="[&lt;strong&gt;KSAUDIO_DYNAMIC_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range)"><strong>KSAUDIO_DYNAMIC_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSAUDIO 类型的结构\_动态\_范围，该范围指定响度节点的输出流的动态范围。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_动态\_范围属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

默认情况下，\_动态\_范围结构的 KSAUDIO 的**QuietCompression**和**LoudCompression**成员的值设置为零%。 这会生成音频流的完整动态范围。 小型端口驱动程序在实例化其数据路径包含节点的固定值时，将属性设置为其默认值。

某些设备可能不支持对**QuietCompression**和**LoudCompression**的更改。 如果客户端尝试更改设备不支持的值，微型端口驱动程序应返回错误。

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

[**KSNODETYPE\_响度**](ksnodetype-loudness.md)

[**KSAUDIO\_动态\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_dynamic_range)

 

 






