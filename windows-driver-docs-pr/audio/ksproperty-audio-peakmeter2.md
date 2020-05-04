---
title: KSPROPERTY\_音频\_PEAKMETER2
description: Windows 8 引入了 KSPROPERTY\_AUDIO\_PEAKMETER2 属性，该属性报告自上次重置 peakmeter 节点后 peakmeter 节点（KSNODETYPE\_peakmeter）上出现的最大音频信号级别。
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
ms.date: 04/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: bf6041ef504e1bf7c074eec21bd47ab8da61da6a
ms.sourcegitcommit: 8f27122409dea11ef0635afbbe5788a648066a1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81772729"
---
# <a name="ksproperty_audio_peakmeter2"></a>KSPROPERTY\_音频\_PEAKMETER2

Windows 8 引入了 KSPROPERTY\_AUDIO\_PEAKMETER2 属性，该属性报告自上次重置 peakmeter 节点后 peakmeter 节点（KSNODETYPE\_peakmeter）上出现的最大音频信号级别。

## <span id="ddk_ksproperty_audio_peakmeter2_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER2_KS"></span>


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
<td align="left"><p>节点 via 筛选器或固定实例</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>


属性值（操作数据）的类型为 LONG，并指定节点上的峰值示例值。 如果峰值值为负数，则使用其绝对值。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_PEAKMETER2 属性请求返回状态\_"成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了可能的错误状态代码。

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
<td align="left"><p>KS 筛选器无法返回当前的 peakmeter 值。</p></td>
</tr>
</tbody>
</table>


<a name="remarks"></a>备注
-------

KSPROPERTY\_音频\_PEAKMETER2 属性与[**\_KSPROPERTY 音频\_PEAKMETER**](ksproperty-audio-peakmeter.md)属性几乎相同。 Windows 8\_中\_引入了 KSPROPERTY AUDIO PEAKMETER2 属性，以提供已改进的 pin 拓扑硬件计数。 旧的 KSPROPERTY\_AUDIO\_PEAKMETER 属性已弃用，不应再使用。

SignedMinimum 必须设置为长\_分钟（而不是0x8000），而 SignedMaximum 必须设置为\_最大值（而不是0x7fff）。 另外，请注意，峰值计量器值是相对于此刻度的，刻度是线性的。

例如，如果您有一个波形在-1 和 + 1 上分别分别为-1 和 + 1 （在从-1 到 + 1 的刻度上），则\_最大的峰值计量值将准确报告给定时间窗口的最大波形值。 相反，应使用最大值为零（0）的峰值计量器来报告无声，其中所有波形值都为零。 但对于其峰值值*介于*零（0）和\_最大值之间的波形，所报告的波形值将从原始中线性减小。

因此，对于介于-0.5 和 + 0.5 之间的波形（在从-1 到 + 1 的刻度上），峰值计量器值必须设置为 "长\_MAX/2"。

KS 音频筛选器以同步方式处理此属性请求。 如果请求成功，则将重置 peakmeter，这会将累积的峰值值初始化为零。 如果请求未成功，则不会更改 peakmeter。

系统会为 IRQL 被动\_\_级别\_的 KSPROPERTY\_AUDIO\_PEAKMETER2 属性发送 IOCTL KS 属性请求。

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

[**KSNODEPROPERTY\_音频\_通道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

[**KSPROPERTY\_音频\_PEAKMETER**](ksproperty-audio-peakmeter.md)
