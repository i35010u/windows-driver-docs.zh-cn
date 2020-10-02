---
title: KSPROPERTY \_ 音频 \_ MUX \_ 源
description: KSPROPERTY \_ 音频 \_ MUX \_ source 属性指定多路复用器的输出流的源。 这是 MUX 节点 (KSNODETYPE MUX) 的属性 \_ 。
ms.assetid: 631d12f2-3f30-4d3e-a0b2-731634858897
keywords:
- KSPROPERTY_AUDIO_MUX_SOURCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MUX_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e94adb3aa88e8a8ec8bbbaa09fea0bface3558c9
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91645965"
---
# <a name="ksproperty_audio_mux_source"></a>KSPROPERTY \_ 音频 \_ MUX \_ 源


KSPROPERTY \_ 音频 \_ MUX \_ source 属性指定多路复用器的输出流的源。 这是 MUX 节点 ([**KSNODETYPE \_ MUX**](ksnodetype-mux.md)) 的属性。

## <span id="ddk_ksproperty_audio_mux_source_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MUX_SOURCE_KS"></span>


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
<td align="left"><p>筛选器</p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型。 此值是 MUX 节点上所选输入插针的 pin ID。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ MUX \_ 源属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>注解
-------

Pin ID 标识 MUX 节点上的逻辑 pin。 有关筛选器内某个节点上的逻辑插针 Id 的讨论，请参阅 [**PCCONNECTION \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcconnection_descriptor)。

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


[**KSNODETYPE \_ MUX**](ksnodetype-mux.md)

[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**PCCONNECTION \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcconnection_descriptor)

