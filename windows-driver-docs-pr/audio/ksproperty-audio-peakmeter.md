---
title: KSPROPERTY\_音频\_PEAKMETER
description: KSPROPERTY\_AUDIO\_PEAKMETER 属性检索自上次重置 PEAKMETER 节点后 PEAKMETER 节点（KSNODETYPE\_PEAKMETER）上出现的最大音频信号级别。
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
ms.openlocfilehash: 2a041d558b9e14007ee660beeb2016a3ddf5362b
ms.sourcegitcommit: 8f27122409dea11ef0635afbbe5788a648066a1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81772735"
---
# <a name="ksproperty_audio_peakmeter"></a>KSPROPERTY\_音频\_PEAKMETER

KSPROPERTY\_AUDIO\_PEAKMETER 属性检索自上次重置 PEAKMETER 节点后 PEAKMETER 节点（[**\_KSNODETYPE PEAKMETER**](ksnodetype-peakmeter.md)）上出现的最大音频信号级别。

>>
> [!IMPORTANT]
> KSPROPERTY\_AUDIO\_PEAKMETER 属性是折旧的，不应使用。 改[**为\_使用\_KSPROPERTY AUDIO PEAKMETER2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-peakmeter2) 。  


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

KSPROPERTY\_音频\_PEAKMETER 属性请求返回状态\_"成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了可能的错误状态代码。

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

系统会为 IRQL 被动\_\_级别\_的 KSPROPERTY\_AUDIO\_PEAKMETER 属性发送 IOCTL KS 属性请求。

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

[**KSPROPERTY\_音频\_PEAKMETER2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-peakmeter2)
