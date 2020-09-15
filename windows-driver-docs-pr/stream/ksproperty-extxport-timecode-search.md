---
title: KSPROPERTY \_ EXTXPORT 时间 \_ 码 \_ 搜索
description: KSPROPERTY \_ EXTXPORT 时间 \_ 码 \_ 搜索属性搜索特定时间码。
ms.assetid: 34252fce-426b-4f75-b57f-fa86654ffc5f
keywords:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85542274513ccf33a102ae1d0545b3344256d29d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102698"
---
# <a name="ksproperty_extxport_timecode_search"></a>KSPROPERTY \_ EXTXPORT 时间 \_ 码 \_ 搜索


KSPROPERTY \_ EXTXPORT 时间 \_ 码 \_ 搜索属性搜索特定时间码。

## <span id="ddk_ksproperty_extxport_timecode_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_TIMECODE_SEARCH_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>设备</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>嵌入时间 <strong>码</strong> 结构</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是 KSPROPERTY EXTXPORT S 结构的嵌入时间 **码** 结构成员 \_ ，用于 \_ 描述要搜索的特定时间码，包括帧、秒、分钟和小时。

<a name="remarks"></a>备注
-------

定义了此方法，但不支持此方法。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

