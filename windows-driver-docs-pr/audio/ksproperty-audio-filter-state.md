---
title: KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态
description: KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态属性用于查询 GFX 筛选器，以获取它支持的属性集的列表。 列表以属性集 Guid 数组的形式进行检索。
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
ms.openlocfilehash: 682d32db80c86a7f94fd6962f71f780a811a775b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102110"
---
# <a name="ksproperty_audio_filter_state"></a>KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态


KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态属性用于查询 GFX 筛选器，以获取它支持的属性集的列表。 列表以属性集 Guid 数组的形式进行检索。

## <span id="ddk_ksproperty_audio_filter_state_ks"></span><span id="DDK_KSPROPERTY_AUDIO_FILTER_STATE_KS"></span>


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
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>Guid 数组</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性数据是一个 Guid 数组。 数组中的每个 GUID 指定筛选器支持的属性集。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性返回的 Guid 数组的大小取决于筛选器支持的属性集数。 在检索该数组之前，客户端首先会通过使用长度为零的属性值缓冲区发送微型端口驱动程序的属性处理程序 KSPROPERTY 的 \_ 音频 \_ 筛选器 \_ 状态 get 属性请求，来查询属性的 GUID 数组的大小。 处理程序通过返回所需的缓冲区大小和状态代码状态缓冲区溢出来做出响应 \_ \_ 。 有关详细信息，请参阅 [音频属性处理程序](./audio-property-handlers.md)。

使用 KSPROPERTY \_ 音频 \_ 筛选器 \_ 状态 get-属性请求中的 guid 数组，操作系统可以按顺序询问每个属性集中的属性。 使用此信息，操作系统可以在实例化筛选器时还原 GFX 筛选器对象的状态，还可以在筛选器销毁时保存 GFX 筛选器对象的状态。 保存或还原 GFX 筛选器的状态时，操作系统会按照 [KS 属性](../stream/ks-properties.md)中所述，对每个属性集中的属性的请求进行序列化。 保存和还原 GFX 筛选器状态的目的是保留用户对筛选器设置所做的任何更改，并使设置在筛选器的连续实例化后保持不变。 .

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

