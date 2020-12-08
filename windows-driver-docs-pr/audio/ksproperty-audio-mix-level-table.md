---
title: KSPROPERTY \_ AUDIO \_ 混音 \_ 级 \_ 表
description: KSPROPERTY \_ AUDIO \_ MIX \_ LEVEL LEVEL \_ TABLE 属性指定 supermixer 节点 (KSNODETYPE SUPERMIX) 的组合级别 \_ 。 它提供所有输入和输出通道的信息。
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
ms.date: 09/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: f43986487cda280be9757e944b7991f451ceb892
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784513"
---
# <a name="ksproperty_audio_mix_level_table"></a>KSPROPERTY \_ AUDIO \_ 混音 \_ 级 \_ 表


KSPROPERTY \_ AUDIO \_ MIX \_ LEVEL LEVEL \_ TABLE 属性指定 supermixer 节点 ([**KSNODETYPE \_ SUPERMIX**](ksnodetype-supermix.md)) 的组合级别。 它提供所有输入和输出通道的信息。

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
<td align="left"><p>可选</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXLEVEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)"><strong>KSAUDIO_MIXLEVEL</strong></a>结构的数组</p></td>
</tr>
</tbody>
</table>

节点需要实现对 KSPROPERTY TYPE_GET 请求的支持 \_ 。 但是，支持 KSPROPERTY \_ 类型 \_ 集的请求是可选的。

 (操作数据) 的属性值是一个 KSAUDIO \_ MIXLEVEL 结构的数组，该数组指定 \* supermixer 节点中所有 m N 输入输出路径的混合级别（带有 M 输入通道和 N 个输出通道）。 数组包含 M \* N 元素：

```cpp
  KSAUDIO_MIXLEVEL  MixLevel[M*N];
```

下表显示了将数组元素映射到 supermixer 节点的 M \* N 输入输出路径。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Array 元素</th>
<th align="left">Input-Output 路径</th>
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

如果没有路径将输入通道 *i* 连接到输出通道 *j*，则筛选器应将数组元素 MixLevel 的 **静音** 成员设置 \[ *i* \* *j* \] 为 **TRUE**。

KSAUDIO MIXLEVEL 数组的大小 \_ 是从从 [**KSPROPERTY \_ 音频 \_ 混音 \_ 级别 \_ 帽**](ksproperty-audio-mix-level-caps.md)检索到的 [**KSAUDIO \_ MIXCAP \_ 表**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)结构计算而来的。 如果结构的 **InputChannels** 和 **OutputChannels** 成员包含值 *m* 和 *n*，则数组大小为

*m* \* *n* \* **sizeof** (KSAUDIO \_ MIXLEVEL) 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 组合 \_ 级别 \_ 表属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此筛选器将成功 \_ \_ \_ \_ 指定组合级别值 (**level** 成员 of KSAUDIO \_ MIXLEVEL) 超出了筛选器的范围，但 (会以) 静默方式将值设置为支持的范围。 但是，在后续请求中获取此属性时，筛选器将输出所使用的实际值。

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


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSAUDIO \_ MIXCAP \_ 表**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSPROPERTY \_ 音频 \_ 混合 \_ 电平 \_**](ksproperty-audio-mix-level-caps.md)

[**KSAUDIO \_ MIXLEVEL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSNODETYPE \_ SUPERMIX**](ksnodetype-supermix.md)

