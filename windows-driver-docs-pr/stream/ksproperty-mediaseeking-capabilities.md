---
title: KSPROPERTY\_MEDIASEEKING\_功能
description: KSPROPERTY\_MEDIASEEKING\_功能属性检索筛选器的媒体搜寻功能。
ms.assetid: f0ee8fed-cdb5-44f9-96c3-d6edf235ea35
keywords:
- KSPROPERTY_MEDIASEEKING_CAPABILITIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_CAPABILITIES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b483e365e8fcb36f1994daf5bb871882475939d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838048"
---
# <a name="ksproperty_mediaseeking_capabilities"></a>KSPROPERTY\_MEDIASEEKING\_功能


KSPROPERTY\_MEDIASEEKING\_功能属性检索筛选器的媒体搜寻功能。

## <span id="ddk_ksproperty_mediaseeking_capabilities_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_CAPABILITIES_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>KS_SEEKING_CAPABILITIES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性检索的筛选器的功能包括：查找绝对位置、在媒体中向前或向后查找、在播放或停止模式下获取当前位置、获取持续时间或向后播放。 请注意，这些是整个筛选器的功能;此属性旨在映射到 DirectShow 查找功能，其中仅对筛选器（而不是 pin）查询此类功能。

如果此属性不受支持，则假定筛选器不需要位置信息，并且筛选器可以视为通过。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






