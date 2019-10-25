---
title: KSPROPERTY\_音频\_EQ\_波段
description: KSPROPERTY\_音频\_EQ\_波段属性指定均衡表中的一组频率带区。 这是 EQ 节点中通道的一个 "获取" 属性（KSNODETYPE\_均衡器）。
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
ms.openlocfilehash: 9e74286a26dc1696d10cbf6789d3b208b27f8351
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831037"
---
# <a name="ksproperty_audio_eq_bands"></a>KSPROPERTY\_音频\_EQ\_波段


KSPROPERTY\_音频\_EQ\_波段属性指定均衡表中的一组频率带区。 这是 EQ 节点中通道的一个 "获取" 属性（[**KSNODETYPE\_均衡**](ksnodetype-equalizer.md)器）。

## <span id="ddk_ksproperty_audio_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_BANDS_KS"></span>


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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>ULONG 数组</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 ULONG 元素数组：

```cpp
  ULONG  CenterFreqVal[N];
```

如果通道的均衡表包含 N 个频带的条目，则数组包含 N 个元素，每个数组元素指定相应带区的中心频率。 微型端口驱动程序将以赫兹（Hz）表示的整数 frequency 值写入每个元素。 下表显示了为数组元素分配均衡带区的情况。

数组元素说明 CenterFreqVal\[0\]

均衡波段0的中心频率（以赫兹为赫兹）。

CenterFreqVal\[1\]

均衡波段1的中心频率（以 Hz 为赫兹）。

...

CenterFreqVal\[N-1\]

均衡波段 N-1 的中心频率（以 Hz 为赫兹）。

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_EQ\_波段属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

可以通过先提交[**KSPROPERTY\_音频\_NUM\_EQ\_波段**](ksproperty-audio-num-eq-bands.md)请求来确定均衡波段的数目。

频率带区的均衡级别由[**KSPROPERTY\_音频\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)属性指定。

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

[**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY\_音频\_NUM\_EQ\_带区**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_音频\_EQ\_级别**](ksproperty-audio-eq-level.md)

 

 






