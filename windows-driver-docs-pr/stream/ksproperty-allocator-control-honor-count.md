---
title: KSPROPERTY \_ 分配器 \_ 控制 \_ 服从 \_ 计数
description: KSPROPERTY \_ 分配器 \_ 控制 \_ 服从 \_ 计数属性通知覆盖混音器如何确定要分配的 DirectDraw 表面的数目。 此属性是可选的。
ms.assetid: 3a867554-a6ef-49bd-89e7-e5d09a21609e
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c879d7fafcb83fb175c037313e19e185c8a2cb8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102406"
---
# <a name="ksproperty_allocator_control_honor_count"></a>KSPROPERTY \_ 分配器 \_ 控制 \_ 服从 \_ 计数


KSPROPERTY \_ 分配器 \_ 控制 \_ 服从 \_ 计数属性通知覆盖混音器如何确定要分配的 DirectDraw 表面的数目。 此属性是可选的。

## <span id="ddk_ksproperty_allocator_control_honor_count_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是一个 DWORD，用于指定覆盖混音器计算覆盖曲面数量和使用的方式。

<a name="remarks"></a>备注
-------

KSPROPERTY \_ 分配器 \_ 控制 \_ 服从 \_ 计数属性请求必须返回1才能强制覆盖混音器使用 [**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md) 属性中指定的图面数。 返回值为零将导致覆盖混音器计算要分配的表面数。

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

[**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

