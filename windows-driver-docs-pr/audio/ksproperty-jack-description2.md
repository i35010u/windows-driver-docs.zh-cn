---
title: KSPROPERTY \_ 插座 \_ DESCRIPTION2
description: KSPROPERTY \_ 插座 \_ DESCRIPTION2 属性实现为使用筛选器句柄访问的基于 pin 的属性。
ms.assetid: 6856060b-f735-4ed8-99bd-5896c87d581f
keywords:
- KSPROPERTY_JACK_DESCRIPTION2 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5939200b7bb56ce7f6c95c4f63b90b56b813bfa6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210967"
---
# <a name="ksproperty_jack_description2"></a>KSPROPERTY \_ 插座 \_ DESCRIPTION2


KSPROPERTY \_ 插座 \_ DESCRIPTION2 属性实现为使用筛选器句柄访问的基于 pin 的属性。

在 Windows 7 和更高版本的 Windows 操作系统中，此属性可在与一个或多个物理插孔关联的任何桥插针上受到支持。 KSPROPERTY \_ 插座 \_ DESCRIPTION2 用于获取设备的状态和与插孔相关的功能。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a> 后跟 <a href="ksjack-description2.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION2&lt;/strong&gt;](ksjack-description2.md)"><strong>KSJACK_DESCRIPTION2</strong></a> 结构的数组</p></td>
</tr>
</tbody>
</table>

 

实例数据)  (属性值为 KSMULTIPLE \_ 项，后跟 KSJACK \_ DESCRIPTION2 结构的数组。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 插座 \_ DESCRIPTION2 属性请求返回 KSMULTIPLE \_ 项，后跟 *n* KSJACK DESCRIPTION2 结构的数组 \_ ，其中 *n* = 与指定桥接器关联的插孔数。 以下列表显示了属性请求返回的项。

KSMULTIPLE \_ 项。Size = sizeof (KSMULTIPLE \_ 项) + N \* SIZEOF (KSJACK \_ DESCRIPTION2) 

KSMULTIPLE \_ 项。计数 = N

KSJACK \_ DESCRIPTION2 \[ 0\]

...

KSJACK \_ DESCRIPTION2 \[\]

<a name="remarks"></a>备注
-------

每个 KSJACK \_ DESCRIPTION2 结构都必须只包含一个插孔的相关信息。

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
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK \_ DESCRIPTION2**](ksjack-description2.md)

[KSMULTIPLE \_ 项](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

