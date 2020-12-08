---
title: KSPROPERTY \_ 音频 \_ EQ \_ 级别
description: KSPROPERTY \_ AUDIO \_ EQ \_ LEVEL 属性指定包含 n 个 frequency 区段条目的均衡表的均衡级别。 这是 (KSNODETYPE 均衡器) 的 EQ 节点中通道的属性 \_ 。
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
ms.openlocfilehash: c5cb6f8c98f31b6b951bcaae9620b2d6e4970ee0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784521"
---
# <a name="ksproperty_audio_eq_level"></a>KSPROPERTY \_ 音频 \_ EQ \_ 级别


KSPROPERTY \_ AUDIO \_ EQ \_ LEVEL 属性指定包含 *n* 个 frequency 区段条目的均衡表的均衡级别。 这是 ([**KSNODETYPE \_ 均衡**](ksnodetype-equalizer.md) 器) 的 EQ 节点中通道的属性。

## <span id="ddk_ksproperty_audio_eq_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_LEVEL_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>长数组</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个长元素数组：

```cpp
  LONG  Level[N];
```

如果通道的均衡表中包含 N 个频带的条目，则数组包含 N 个元素，每个元素指定一个用于均衡表的带区级别。 下表显示了为数组元素分配带区的情况。

数组元素说明级别 \[ 0\]

波段0的级别。

级别 \[ 1\]

波段1的级别。

...

级别 \[ N-1\]

波段 N-1 级别。

 

级别值使用以下比例：

-2147483648 是-无限大 (衰减) ，

-2147483647 是-32767.99998474 分贝 (衰减) ，

+ 2147483647 为 + 32767.99998474 分贝 (获取) 。

由整数值（2147483648到 + 2147483647）表示的分贝范围，其中

此刻度的分辨率为1/65536 分贝。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ EQ \_ LEVEL 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此筛选器将成功 \_ 指定一个 \_ \_ 值，它指定的值超出了筛选器的范围，但会将该值固定到受支持的范围。 但在后续请求中，此属性将输出所使用的实际值。

可以通过首先提交 [**KSPROPERTY 的 \_ 音频 \_ 号 \_ EQ \_ 波段**](ksproperty-audio-num-eq-bands.md) 请求来确定均衡波段的数目。

均衡波段的中心频率由 [**KSPROPERTY \_ AUDIO \_ EQ \_ 波段**](ksproperty-audio-eq-bands.md) 属性指定。

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


[**KSNODEPROPERTY \_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE \_ 均衡器**](ksnodetype-equalizer.md)

[**KSPROPERTY \_ 音频 \_ 数字 \_ EQ \_ 带区**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY \_ 音频 \_ EQ \_ 带区**](ksproperty-audio-eq-bands.md)

