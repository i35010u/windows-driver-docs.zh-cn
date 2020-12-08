---
title: KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL
description: KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL 属性指定给定流中通道的音量级别。
keywords:
- KSPROPERTY_AUDIOENGINE_VOLUMELEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_VOLUMELEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6f93b071f631dfbbf05a003416bf3e0b1db2c53
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784429"
---
# <a name="ksproperty_audioengine_volumelevel"></a>KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL


**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL** 属性指定给定流中通道的音量级别。

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
<td align="left"><p>节点 via 引脚实例</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>Get 请求的长 () 和 KSAUDIOENGINE_VOLUMELEVEL 请求的<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_VOLUMELEVEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)"><strong>KSAUDIOENGINE_VOLUMELEVEL</strong></a> () 。</p></td>
</tr>
</tbody>
</table>

 

对于 Get 请求，属性值的类型为 LONG，它指定给定流中通道的卷级别。 卷级别的值使用以下小数位数，可受此属性的基本支持响应中提供的最小值和最大值的限制：

-2147483648 (以十六进制表示的0x80000000，或) 的 LONG \_ 值为-无限大 (衰减) ，

-2147483647 (以十六进制表示的0x80000001，或者长 \_ 分钟 + 1) 为-32767.99998474 分贝 (衰减) ，

+ 2147483647 (0x7FFFFFFF，以十六进制表示， \_ 最大) 为 + 32767.99998474 分贝 (获取) 。

> [!NOTE]
> 分贝范围由从-2147483648 到 + 2147483647 的整数值表示，其中此刻度的分辨率为1/65536 分贝。

 

对于设置请求，属性值的类型为 **KSAUDIOENGINE \_ VOLUMELEVEL**，它指定给定流中的通道所需的音量级别，以及要在设置卷级别时应用的曲线类型和曲线持续时间。 如果在筛选器范围之外指定了某个值，则设置此属性的请求仍将成功。 但应用于筛选器的实际值只能由对此属性的后续调用来确定。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

[**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)属性请求返回 **状态 \_ SUCCESS** 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL** 的属性描述符指定频道号。 如果穿过音频引擎节点的流包含 *n* 个通道，通道将从0到 *n-1* 进行编号。 另请注意，如果通道值为0xFFFFFFFF，则表明请求适用于所有通道。 如果在流未处于运行状态时发出了属性请求，则会立即将卷级别设置为请求的级别。 如果流在卷级别斜坡正在进行时仍保持运行状态，则流的卷级别会立即设置为当前淡化的目标级别。 如果在现有的卷级别斜坡正在进行时发出新的属性请求，则新的斜坡请求必须从当前的音量级别开始，即当新请求到达时，已达到了该卷的级别。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOENGINE \_ VOLUMELEVEL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)

[**KSNODEPROPERTY \_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

