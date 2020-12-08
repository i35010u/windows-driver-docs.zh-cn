---
title: KSPROPERTY \_ 音频 \_ EQ \_ 带区
description: KSPROPERTY \_ AUDIO \_ EQ \_ 波段属性指定均衡表中的一组频率带区。 这是 (KSNODETYPE 均衡器) 的 EQ 节点中通道的获取属性 \_ 。
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
ms.openlocfilehash: e5e606bba86970ea7ef53775050ccb019a0b0c7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799039"
---
# <a name="ksproperty_audio_eq_bands"></a>KSPROPERTY \_ 音频 \_ EQ \_ 带区


KSPROPERTY \_ AUDIO \_ EQ \_ 波段属性指定均衡表中的一组频率带区。 这是 ([**KSNODETYPE \_ 均衡**](ksnodetype-equalizer.md) 器) 的 EQ 节点中通道的获取属性。

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
<td align="left"><p>否</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>ULONG 数组</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 ULONG 元素数组：

```cpp
  ULONG  CenterFreqVal[N];
```

如果通道的均衡表包含 N 个频带的条目，则数组包含 N 个元素，每个数组元素指定相应带区的中心频率。 微型端口驱动程序将以赫兹 (Hz) 表示的整数频率值写入每个元素。 下表显示了为数组元素分配均衡带区的情况。

数组元素说明 CenterFreqVal \[ 0\]

均衡波段0的中心频率 (以 Hz) 。

CenterFreqVal \[ 1\]

均衡波段1的中心频率 (以 Hz) 。

...

CenterFreqVal \[ N-1\]

均衡波段 (以 Hz) 的中心频率。

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ EQ \_ 波段属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

可以通过首先提交 [**KSPROPERTY 的 \_ 音频 \_ 号 \_ EQ \_ 波段**](ksproperty-audio-num-eq-bands.md) 请求来确定均衡波段的数目。

频率带区的均衡级别由 [**KSPROPERTY \_ AUDIO \_ EQ \_ LEVEL**](ksproperty-audio-eq-level.md) 属性指定。

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

[**KSPROPERTY \_ 音频 \_ EQ \_ 级别**](ksproperty-audio-eq-level.md)

