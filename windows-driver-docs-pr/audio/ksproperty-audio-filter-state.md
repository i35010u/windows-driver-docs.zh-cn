---
title: KSPROPERTY\_AUDIO\_FILTER\_STATE
description: KSPROPERTY\_音频\_筛选器\_STATE 属性用来查询 GFX 筛选器集，它支持的属性列表。 中的属性集 Guid 数组的形式检索列表。
ms.assetid: e0a3bce7-d321-445c-866c-78502b5ea887
keywords:
- KSPROPERTY_AUDIO_FILTER_STATE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_FILTER_STATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11f4dfcd79e4206bdaa55b569a6df7fd2f7999b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333043"
---
# <a name="kspropertyaudiofilterstate"></a>KSPROPERTY\_AUDIO\_FILTER\_STATE


KSPROPERTY\_音频\_筛选器\_STATE 属性用来查询 GFX 筛选器集，它支持的属性列表。 中的属性集 Guid 数组的形式检索列表。

## <span id="ddk_ksproperty_audio_filter_state_ks"></span><span id="DDK_KSPROPERTY_AUDIO_FILTER_STATE_KS"></span>


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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>Guid 的数组</p></td>
</tr>
</tbody>
</table>

 

属性数据 （操作数据） 是 Guid 的数组。 数组中的每个 GUID 指定某个属性设置筛选器支持。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_筛选器\_状态属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性返回的 Guid 的数组的大小取决于该筛选器支持的属性集的数量。 检索数组之前, 客户端首先查询该属性的 GUID 数组的大小，通过发送 KSPROPERTY 的微型端口驱动程序的属性处理程序\_音频\_筛选器\_状态获取属性请求使用长度为零属性值的缓冲区。 返回所需的缓冲区大小和状态的状态代码响应处理程序\_缓冲区\_溢出。 有关详细信息，请参阅[音频属性处理程序](https://msdn.microsoft.com/library/windows/hardware/ff536214)。

使用 Guid 的数组从 KSPROPERTY\_音频\_筛选器\_状态获取属性请求时，操作系统可以按顺序询问每个属性集内的属性。 此信息使操作系统在实例化筛选器时，时间还原 GFX 筛选器对象的状态以及在筛选器被销毁时保存 GFX 筛选器对象的状态。 当保存或还原 GFX 筛选器的状态时，操作系统将序列化的属性中每个属性集，其请求中所述[KS 属性](https://msdn.microsoft.com/library/windows/hardware/ff567671)。 保存和还原 GFX 筛选器的状态的目的是要保留用户对筛选器的设置，所做的任何更改并使设置在连续的实例化的筛选器。 .

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






