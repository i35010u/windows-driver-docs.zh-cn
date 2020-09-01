---
title: KSPROPERTY \_ 音频 \_ PEAKMETER
description: KSPROPERTY \_ AUDIO \_ PEAKMETER 属性检索 \_ 自上次重置 PEAKMETER 节点后 PEAKMETER 节点上发生的最高音频信号级别 (KSNODETYPE PEAKMETER) 。
ms.assetid: c8c2c9ed-61ea-4bbe-b376-c956f051416e
keywords:
- KSPROPERTY_AUDIO_PEAKMETER 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PEAKMETER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e73fbd5ecc7b5b4c085e1d0974618babf45f642
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206965"
---
# <a name="ksproperty_audio_peakmeter"></a>KSPROPERTY \_ 音频 \_ PEAKMETER

KSPROPERTY \_ AUDIO \_ PEAKMETER 属性检索自上次重置 PEAKMETER 节点后 PEAKMETER 节点上发生的最高音频信号级别 ([**KSNODETYPE \_ PEAKMETER**](ksnodetype-peakmeter.md)) 。

>>
> [!IMPORTANT]
> KSPROPERTY \_ AUDIO \_ PEAKMETER 属性是折旧的，不应使用。 改为使用 [**KSPROPERTY \_ AUDIO \_ PEAKMETER2**](./ksproperty-audio-peakmeter2.md) 。  


## <span id="ddk_ksproperty_audio_peakmeter_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER_KS"></span>


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
<td align="left"><p>节点 via 筛选器或固定实例</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 (操作数据) 的属性值的类型为 LONG，并指定节点上的峰值样本值。 如果峰值值为负数，则使用其绝对值。


### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ PEAKMETER 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了可能的错误状态代码。

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

KS 音频筛选器以同步方式处理此属性请求。 如果请求成功，则将重置 peakmeter，这会将累积的峰值值初始化为零。 如果请求未成功，则不会更改 peakmeter。

系统会 \_ \_ 为 \_ IRQL 被动级别的 KSPROPERTY AUDIO PEAKMETER 属性发送 IOCTL KS 属性请求 \_ \_ 。

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

[**KSNODETYPE \_ PEAKMETER**](ksnodetype-peakmeter.md)

[**KSPROPERTY \_ 音频 \_ PEAKMETER2**](./ksproperty-audio-peakmeter2.md)