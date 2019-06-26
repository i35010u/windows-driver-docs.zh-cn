---
title: KSPROPERTY\_AUDIO\_EQ\_LEVEL
description: KSPROPERTY\_音频\_EQ\_级别属性指定包含 n 频率带区的条目的均衡表的均衡级别。 这是 EQ 节点中的通道的属性 (KSNODETYPE\_均衡器)。
ms.assetid: 17c34af2-dbeb-472c-9825-9dc64f7f96bd
keywords:
- KSPROPERTY_AUDIO_EQ_LEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_EQ_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: da75ddf62f6c75e95a56ff33cd6972381f49e611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358926"
---
# <a name="kspropertyaudioeqlevel"></a>KSPROPERTY\_AUDIO\_EQ\_LEVEL


KSPROPERTY\_音频\_EQ\_级别属性指定包含的条目的均衡表的均衡级别*n*频率带区。 这是 EQ 节点中的通道的属性 ([**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md))。

## <span id="ddk_ksproperty_audio_eq_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_LEVEL_KS"></span>


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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>长整型数组</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是较长的元素的数组：

```cpp
  LONG  Level[N];
```

如果通道的均衡表包含 N 频率带区的条目，该数组包含 N 个元素和每个元素指定一个带区级别均衡表中。 下表中显示为数组元素的带区的分配。

数组元素说明级别\[0\]

针对带 0 的级别。

级别\[1\]

针对带 1 级别。

...

级别\[N-1\]

针对带 N-1 级别。

 

级别值使用以下等级：

是-2147483648-无穷大分贝 （衰减）

在-2147483647 是-32767.99998474 分贝 （衰减） 和

+2147483647 是 +32767.99998474 分贝 （提升）。

由整数值介于-2147483648 到 +2147483647，表示分贝范围位置

此范围具有的分辨率为 1/65536 分贝。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_EQ\_级别属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

筛选器将会成功 KSPROPERTY\_音频\_EQ\_级别指定的值超出范围的筛选器，但将固定到支持的范围值的组属性请求。 在后续请求中获取此属性，但是，它将输出所用的实际值。

均衡带区的数目可以由第一个提交[ **KSPROPERTY\_音频\_NUM\_EQ\_带区**](ksproperty-audio-num-eq-bands.md)请求。

指定的均衡带区的中心频率[ **KSPROPERTY\_音频\_EQ\_带区**](ksproperty-audio-eq-bands.md)属性。

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

 

 






