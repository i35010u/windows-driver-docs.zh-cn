---
title: KSPROPERTY \_ MEDIASEEKING \_ 功能
description: KSPROPERTY \_ MEDIASEEKING \_ 功能属性检索筛选器的媒体搜寻功能。
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
ms.openlocfilehash: 06830abbfb115fbe3b54bffafbcd93fd7c38c23d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103550"
---
# <a name="ksproperty_mediaseeking_capabilities"></a>KSPROPERTY \_ MEDIASEEKING \_ 功能


KSPROPERTY \_ MEDIASEEKING \_ 功能属性检索筛选器的媒体搜寻功能。

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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[KSPROPSETID \_ MediaSeeking](kspropsetid-mediaseeking.md)

