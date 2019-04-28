---
title: KSPROPERTY\_音频\_PEAKMETER
description: KSPROPERTY\_音频\_PEAKMETER 属性检索 peakmeter 节点处出现的最大的音频信号级别 (KSNODETYPE\_PEAKMETER) 自上次 peakmeter 节点已重置。
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
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437d24da91f7fb3f40f12b13e5529c8de35797e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332916"
---
# <a name="kspropertyaudiopeakmeter"></a>KSPROPERTY\_音频\_PEAKMETER


KSPROPERTY\_音频\_PEAKMETER 属性检索 peakmeter 节点处出现的最大的音频信号级别 ([**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md))自上次 peakmeter 节点已重置。

## <span id="ddk_ksproperty_audio_peakmeter_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER_KS"></span>


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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 long 类型的值，指定在节点上的峰值示例值。 如果峰值值为负，则使用其绝对值的数值。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_PEAKMETER 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。 下表显示了可能的错误状态代码。

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

 

 






