---
title: KSPROPERTY\_AUDIO\_MIX\_LEVEL\_TABLE
description: KSPROPERTY\_音频\_混合\_级别\_表属性指定 supermixer 节点的混合级别 (KSNODETYPE\_SUPERMIX)。 它提供所有输入和输出通道的信息。
ms.assetid: 1a1b486b-06e4-462b-8fe9-9d3581c82d06
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_TABLE Audio Devices
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
ms.openlocfilehash: 3e05e4e922e08ee31a90b535a7f80923a7b18459
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358911"
---
# <a name="kspropertyaudiomixleveltable"></a>KSPROPERTY\_AUDIO\_MIX\_LEVEL\_TABLE


KSPROPERTY\_音频\_混合\_级别\_表属性指定 supermixer 节点的混合级别 ([**KSNODETYPE\_SUPERMIX** ](ksnodetype-supermix.md)). 它提供所有输入和输出通道的信息。

## <span id="ddk_ksproperty_audio_mix_level_table_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_TABLE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>数组<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXLEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel)"> <strong>KSAUDIO_MIXLEVEL</strong> </a>结构</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个数组 KSAUDIO\_MIXLEVEL 结构，它指定所有 M 组合级别\*M supermixer 节点中的第 N 输入输出路径输入通道和 N 输出通道。 该数组包含 M\*N 个元素：

```cpp
  KSAUDIO_MIXLEVEL  MixLevel[M*N];
```

下表显示的数组元素映射到 supermixer 节点 M\*N 输入输出路径。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">数组元素</th>
<th align="left">输入-输出路径</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MixLevel[0]</p></td>
<td align="left"><p>输入通道输出通道 0 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel[1]</p></td>
<td align="left"><p>输入通道 0 到输出通道 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel[N-1]</p></td>
<td align="left"><p>输入到输出通道 N-1 通道 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel[N]</p></td>
<td align="left"><p>输入通道 1 到输出通道 0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel[N+1]</p></td>
<td align="left"><p>输入通道 1 到输出通道 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel[2N-1]</p></td>
<td align="left"><p>输入到输出通道 N-1 通道 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel[M*N-1]</p></td>
<td align="left"><p>输入到输出通道 N-1 M-1 通道</p></td>
</tr>
</tbody>
</table>

 

下图说明了 MixLevel 数组元素与输入输出路径的映射。 控制每个输入-输出路径 MixLevel 数组元素的索引是显示在方括号中。

![说明 supermixer 节点的 mixlevel 数组元素的映射的关系图](images/supermix.png)

如果没有路径连接输入的通道*我*向输出通道*j*，应设置的筛选器**静音**成员的数组元素 MixLevel\[*我* \*N +*j* \]到**TRUE**。

大小 KSAUDIO\_MIXLEVEL 数组计算从[ **KSAUDIO\_MIXCAP\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixcap_table)结构，它从检索[ **KSPROPERTY\_音频\_混合\_级别\_CAPS**](ksproperty-audio-mix-level-caps.md)。 如果该结构的**InputChannels**和**OutputChannels**成员包含值*m*并*n*，数组大小

*m* \* *n* \* **sizeof**(KSAUDIO\_MIXLEVEL)

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_混合\_级别\_表属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

筛选器将会成功 KSPROPERTY\_音频\_混合\_级别\_指定混级别值的表集属性请求 (**级别**KSAUDIO 成员\_MIXLEVEL)，超出了范围的筛选器，但会 （以无提示方式） 将支持的范围的值。 但是，在后续请求中获取此属性，该筛选器将输出所用的实际值。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSAUDIO\_MIXCAP\_TABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_CAPS**](ksproperty-audio-mix-level-caps.md)

[**KSAUDIO\_MIXLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

 

 






