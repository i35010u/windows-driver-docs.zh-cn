---
title: KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL
description: KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL 属性给定流中指定的通道的卷级别。
ms.assetid: E10E2ADC-BD76-4871-85DA-19385A0D77EE
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
ms.openlocfilehash: 5d1276709c02ff3c56b27c52ed6b48a967c1f587
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543167"
---
# <a name="kspropertyaudioenginevolumelevel"></a>KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL


**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**属性给定流中指定的通道的卷级别。

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
<td align="left"><p>通过 Pin 实例的节点</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>长时间 （对于 Get 请求） 和<a href="https://msdn.microsoft.com/library/windows/hardware/hh831854" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_VOLUMELEVEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh831854)"> <strong>KSAUDIOENGINE_VOLUMELEVEL</strong> </a> （适用于 Set 请求）。</p></td>
</tr>
</tbody>
</table>

 

对于 Get 请求，属性的值为 LONG 类型，并指定通道在卷级别对于给定的流。 音量级别值使用以下等级，并可以受此属性的基本支持响应中提供的最小值和最大值：

介于-2147483648 (十六进制或长时间中的 0x80000000\_最小值) 是-无穷大分贝 （衰减）

在-2147483647 (十六进制或长时间中的 0x80000001\_分钟 + 1) 是-32767.99998474 分贝 （衰减） 和

+2147483647 (十六进制或长时间中的 0x7FFFFFFF\_最大值) 是 +32767.99998474 分贝 （提升）。

&gt; \[!请注意\]&gt;分贝范围由整数值表示从-2147483648 到 +2147483647，其中此范围具有的分辨率为 1/65536 分贝。

 

对于组的请求，属性值为类型**KSAUDIOENGINE\_VOLUMELEVEL**，并在给定的流，以及该曲线类型和曲线时间，将应用与卷指定一个通道的所需的卷级别级别设置。 如果超出范围的筛选器指定的值，则设置此属性的请求仍会成功。 仅可确定已应用于筛选器的实际值，但对此属性的后续 Get 调用。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

[ **KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS** ](ksproperty-audioengine-supporteddeviceformats.md)属性请求返回**状态\_成功**到指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

属性描述符**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**指定频道号。 如果通过音频引擎节点流中所包含*n*通道，通道是编号从的 0 到*n-1*。 另请注意，通道值为 0xFFFFFFFF 表示请求应用于所有通道。 如果属性请求时，流未处于运行状态时，音量级别是立即设置为所请求的级别。 如果流离开运行的状态，在进行卷级负载增加时，流的音量级别立即设置为当前的淡入淡出的目标级别。 如果正在现有卷级别负载增加时发出新的属性请求，新的负载增加请求必须以从当前的音量级别的新请求到达时，已达到卷的级别。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOENGINE\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/hh831854)

[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

 

 






