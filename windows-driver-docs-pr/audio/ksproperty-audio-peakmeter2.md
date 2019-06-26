---
title: KSPROPERTY\_AUDIO\_PEAKMETER2
description: Windows 8 引入了 KSPROPERTY\_音频\_PEAKMETER2 报告发生了 peakmeter 节点的最大的音频信号级别的属性 (KSNODETYPE\_PEAKMETER) 自上次 peakmeter 节点已重置。
ms.assetid: 0A59A482-476D-412C-8D15-D821357C355B
keywords:
- KSPROPERTY_AUDIO_PEAKMETER2 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PEAKMETER2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1357db2f34d5219cff1009369b0f4534c487bc34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360599"
---
# <a name="kspropertyaudiopeakmeter2"></a>KSPROPERTY\_AUDIO\_PEAKMETER2


Windows 8 引入了 KSPROPERTY\_音频\_PEAKMETER2 报告发生了 peakmeter 节点的最大的音频信号级别的属性 (KSNODETYPE\_PEAKMETER) 自上次 peakmeter 节点已重置。

## <span id="ddk_ksproperty_audio_peakmeter2_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER2_KS"></span>


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
<td align="left"><p>通过筛选器或 Pin 实例的节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 long 类型的值，指定在节点上的峰值示例值。 如果峰值值为负，则使用其绝对值的数值。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_PEAKMETER2 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了可能的错误状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_IMPLEMENTED</p></td>
<td align="left"><p>KS 筛选器不能返回 peakmeter 的当前值。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_音频\_PEAKMETER2 属性是几乎完全相同[ **KSPROPERTY\_音频\_PEAKMETER** ](ksproperty-audio-peakmeter.md)属性。 KSPROPERTY\_音频\_PEAKMETER2 属性引入了 Windows 8 和更高版本操作系统以提供更强的硬件计数的固定拓扑。 旧 KSPROPERTY\_音频\_PEAKMETER 属性已保留用于向后兼容。

SignedMinimum 必须设置为长时间\_（而不是 0x8000)，最小值和 SignedMaximum 必须设置为长时间\_（而不是 0x7fff) 的最大值。 此外，请注意，峰值计量值是相对于此缩放和规模是线性在 amplitude 中，

因此如果，例如，分别 （上是由从-1 到 + 1 的小数位数） 有与在-1 和 + 1 的负数和正数峰值波形，出现一次峰值计量的长时间值\_最大可准确报告在给定的时间范围的最大波形值。 相反，峰值计量值为零 (0) 应该用于报告无声段，其中的波形的所有值都为零。 但在其最大值是的波形的情况下*之间*零 (0) 和长时间\_最大值，报告的波形值会以线性方式简化从原始文件。

因此，对于-0.5 和 （在上的小数位数是由从-1 到 + 1），+0.5 之间波动峰值曲线波形值必须设置为长时间\_最大/2。

KS 音频筛选器以同步方式处理此属性请求。 如果请求成功，它将重置 peakmeter，这将初始化为零的累计最大资源值。 如果请求不成功，peakmeter 不会更改。

系统发送 IOCTL\_KS\_属性请求 KSPROPERTY\_音频\_PEAKMETER 属性在 IRQL 被动\_级别。

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

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](ksproperty-audio-peakmeter.md)

 

 






