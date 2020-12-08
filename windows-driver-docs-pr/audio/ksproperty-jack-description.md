---
title: KSPROPERTY \_ 插孔 \_ 说明
description: KSPROPERTY \_ 插座 \_ DESCRIPTION 属性作为多项、按固定的属性实现，该属性通过筛选器句柄进行访问。
keywords:
- KSPROPERTY_JACK_DESCRIPTION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6614ac9111f74ee0680dd7e2252cbd2156e99273
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801213"
---
# <a name="ksproperty_jack_description"></a>KSPROPERTY \_ 插孔 \_ 说明


KSPROPERTY \_ 插座 \_ DESCRIPTION 属性作为多项、按固定的属性实现，该属性通过筛选器句柄进行访问。

在 Windows Vista 和更高版本中，此属性可在与一个或多个物理插孔关联的任何桥插针上受到支持。 它用于获取特定插孔的物理特性和使用情况的说明。

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
<td align="left"><p>通过筛选器句柄 (固定工厂) </p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a> 后跟 <a href="ksjack-description.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION&lt;/strong&gt;](ksjack-description.md)"><strong>KSJACK_DESCRIPTION</strong></a> 结构的数组</p></td>
</tr>
</tbody>
</table>

 

实例数据)  (属性值为 KSMULTIPLE \_ 项，后跟 KSJACK \_ 说明结构的数组。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 插座 \_ description 属性请求返回 KSMULTIPLE \_ 项，后跟 *n* KSJACK 说明结构的数组 \_ ，其中 *n* = 与指定桥接器关联的插孔数。 因此，属性请求返回的成员将为：

KSMULTIPLE \_ 项。Size = sizeof (KSMULTIPLE \_ 项) + N \* SIZEOF (KSJACK \_ 说明) 

KSMULTIPLE \_ 项。计数 = N

KSJACK \_ 说明 \[ 0\]

...

KSJACK \_ 说明 \[ N-1\]

<a name="remarks"></a>备注
-------

每个 KSJACK \_ 描述结构都必须包含一个插孔的相关信息。 例如，支持三个立体声插孔的5.1 音频的输出桥插针需要大小为的数据缓冲区

sizeof (KSMULTIPLE \_ 项) + 3 \* SIZEOF (KSJACK \_ 说明) 

每个 KSJACK \_ 描述结构都有一个2位 ChannelMapping 值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK \_ 说明**](ksjack-description.md)

[KSMULTIPLE \_ 项](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[KSPROPERTY](/previous-versions/ff564262(v=vs.85))

