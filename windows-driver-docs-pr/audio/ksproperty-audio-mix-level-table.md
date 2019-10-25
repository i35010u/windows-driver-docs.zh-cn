---
title: KSPROPERTY\_音频\_混合\_级别\_表
description: KSPROPERTY\_音频\_组合\_级别\_表属性为 supermixer 节点指定组合级别（KSNODETYPE\_SUPERMIX）。 它提供所有输入和输出通道的信息。
ms.assetid: 1a1b486b-06e4-462b-8fe9-9d3581c82d06
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_TABLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIX_LEVEL_TABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f932fd125f2d99e8daf5686224957a72f9e38444
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832977"
---
# <a name="ksproperty_audio_mix_level_table"></a>KSPROPERTY\_音频\_混合\_级别\_表


KSPROPERTY\_音频\_组合\_级别\_表属性为 supermixer 节点指定组合级别（[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)）。 它提供所有输入和输出通道的信息。

## <span id="ddk_ksproperty_audio_mix_level_table_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_TABLE_KS"></span>


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
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXLEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)"><strong>KSAUDIO_MIXLEVEL</strong></a>结构的数组</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSAUDIO\_MIXLEVEL 结构的数组，该数组指定 supermixer 节点中所有 M\*N 输入输出路径的混合级别（带有 M 输入通道和 N 个输出通道）。 数组包含 M\*N 个元素：

```cpp
  KSAUDIO_MIXLEVEL  MixLevel[M*N];
```

下表显示了将数组元素映射到 supermixer 节点的 M\*N 输入输出路径。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Array 元素</th>
<th align="left">输入-输出路径</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MixLevel [0]</p></td>
<td align="left"><p>输入通道0到输出通道0</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel [1]</p></td>
<td align="left"><p>输入通道0到输出通道1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel [N-1]</p></td>
<td align="left"><p>输入通道0到输出通道 N-1</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel [N]</p></td>
<td align="left"><p>输入通道1到输出通道0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel [N + 1]</p></td>
<td align="left"><p>输入通道1到输出通道1</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel [2N-1]</p></td>
<td align="left"><p>输入通道1到输出通道 N-1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel [M * N-1]</p></td>
<td align="left"><p>输入通道 M-1 到输出通道 N-1</p></td>
</tr>
</tbody>
</table>

 

下图说明了 MixLevel 数组元素到输入输出路径的映射。 控制每个输入输出路径的 MixLevel 数组元素的索引显示在方括号中。

![说明 supermixer 节点的 mixlevel 数组元素映射的关系图](images/supermix.png)

如果没有路径将输入通道*i*连接到输出通道*j*，则筛选器应将数组元素 MixLevel 的**静音**成员设置\[*i*\*N +*j*\] 设置为**TRUE**。

KSAUDIO\_MIXLEVEL 数组的大小是从[**KSAUDIO\_MIXCAP\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)结构中计算的，该结构是从[**KSPROPERTY\_音频\_混合\_级别\_大写字母**](ksproperty-audio-mix-level-caps.md)检索的。 如果结构的**InputChannels**和**OutputChannels**成员包含值*m*和*n*，则数组大小为

*m* \* *n* \* **sizeof**（KSAUDIO\_MIXLEVEL）

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_混合\_级别\_表属性请求返回状态\_SUCCESS，指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

筛选器将成功\_音频\_混合\_级别\_表集-属性请求，指定超出筛选范围的组合级别**值（KSAUDIO**\_MIXLEVEL），但将（以静默方式）将值固定到支持的范围。 但是，在后续请求中获取此属性时，筛选器将输出所使用的实际值。

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

[**KSPROPERTY\_音频\_混合\_级别\_CAP**](ksproperty-audio-mix-level-caps.md)

[**KSAUDIO\_MIXLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

 

 






