---
title: KSPROPERTY \_ 横线 \_ 可以 \_ 路由
description: KSPROPERTY \_ 纵横制 \_ CAN \_ 路由属性检索设备是否能够支持指定的路由。 必须实现此属性。
ms.assetid: bb966d0a-6ecf-4bbb-a881-30d468abe220
keywords:
- KSPROPERTY_CROSSBAR_CAN_ROUTE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_CAN_ROUTE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77e021b2c03cfdb133ce800657eefebb7cbee7e4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192153"
---
# <a name="ksproperty_crossbar_can_route"></a>KSPROPERTY \_ 横线 \_ 可以 \_ 路由


KSPROPERTY \_ 纵横制 \_ CAN \_ 路由属性检索设备是否能够支持指定的路由。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_can_route_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_CAN_ROUTE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，指定流式处理微型驱动程序是否支持两个 pin 之间的指定路由。 非零值表示支持路由。 如果微型驱动程序不支持两个插针之间的路由，则此值为零。

<a name="remarks"></a>注解
-------

KSPROPERTY **CanRoute** \_ 纵横制路由结构的 CanRoute \_ 成员 \_ 指示该设备是否能够支持指定的路由。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ 横线 \_ 路由 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)

 

