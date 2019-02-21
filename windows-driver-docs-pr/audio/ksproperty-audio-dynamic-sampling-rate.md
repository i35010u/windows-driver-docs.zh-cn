---
title: KSPROPERTY\_AUDIO\_DYNAMIC\_SAMPLING\_RATE
description: KSPROPERTY\_音频\_动态\_采样\_速率属性用于启用和禁用动态跟踪的节点的采样率。
ms.assetid: ff99c670-ef93-4730-8be4-1ed7c01c5381
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa49778ed2903aaa828b198a411008683ec2fa73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524066"
---
# <a name="kspropertyaudiodynamicsamplingrate"></a>KSPROPERTY\_AUDIO\_DYNAMIC\_SAMPLING\_RATE


KSPROPERTY\_音频\_动态\_采样\_速率属性用于启用和禁用动态跟踪的节点的采样率。

## <span id="ddk_ksproperty_audio_dynamic_sampling_rate_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值的类型 BOOL，并指定动态跟踪是启用还是禁用节点上。 值是 **，则返回 TRUE**时启用了动态跟踪的采样率。 可以通过设置通过速率在此模式下，输入的流采样率能显式变化[ **KSPROPERTY\_音频\_采样\_速率**](ksproperty-audio-sampling-rate.md)或隐式通过对输入流设置通过时间戳的速率。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_动态\_采样\_速率属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于控制动态跟踪中的以下节点类型：

-   ADC 节点 ([**KSNODETYPE\_ADC**](ksnodetype-adc.md))

-   DAC 节点 ([**KSNODETYPE\_DAC**](ksnodetype-dac.md))

-   SRC 节点 ([**KSNODETYPE\_SRC**](ksnodetype-src.md))

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSPROPERTY\_AUDIO\_SAMPLING\_RATE**](ksproperty-audio-sampling-rate.md)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

 

 






