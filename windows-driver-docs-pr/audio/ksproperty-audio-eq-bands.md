---
title: KSPROPERTY\_AUDIO\_EQ\_BANDS
description: KSPROPERTY\_音频\_EQ\_带区属性指定的频率均衡表中的带区集。 这是通道 EQ 节点中的一个只读属性 (KSNODETYPE\_均衡器)。
ms.assetid: 64304cad-cf07-4bdb-96d5-7dd594380725
keywords:
- KSPROPERTY_AUDIO_EQ_BANDS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_EQ_BANDS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86f837f9523ecdd8b9847a1a402d74df1f8e3ad4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541617"
---
# <a name="kspropertyaudioeqbands"></a>KSPROPERTY\_AUDIO\_EQ\_BANDS


KSPROPERTY\_音频\_EQ\_带区属性指定的频率均衡表中的带区集。 这是通道 EQ 节点中的一个只读属性 ([**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md))。

## <span id="ddk_ksproperty_audio_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_BANDS_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>ULONG 数组</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 ULONG 元素的数组：

```cpp
  ULONG  CenterFreqVal[N];
```

如果通道的均衡表包含 N 频率带区的条目，该数组包含 N 个元素和每个数组元素指定的相应带区的中心频率。 微型端口驱动程序将以赫兹 (Hz) 表示一个整数频率值写入到的每个元素。 下表中显示于数组元素的均衡带区的分配。

数组元素说明 CenterFreqVal\[0\]

均衡外 0 中心频率 （以 Hz)。

CenterFreqVal\[1\]

均衡外 1 中心频率 （以 Hz)。

...

CenterFreqVal\[N-1\]

均衡外 N-1 中心频率 （以 Hz)。

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_EQ\_带区属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

均衡带区的数目可以由第一个提交[ **KSPROPERTY\_音频\_NUM\_EQ\_带区**](ksproperty-audio-num-eq-bands.md)请求。

指定的均衡级别频段[ **KSPROPERTY\_音频\_EQ\_级别**](ksproperty-audio-eq-level.md)属性。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

 

 






