---
title: KSPROPERTY\_CROSSBAR\_CAN\_ROUTE
description: KSPROPERTY\_纵横制\_可以\_路由属性检索设备是否能够支持指定的路由。 必须实现此属性。
ms.assetid: bb966d0a-6ecf-4bbb-a881-30d468abe220
keywords:
- KSPROPERTY_CROSSBAR_CAN_ROUTE 流式处理媒体设备
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
ms.openlocfilehash: 97f8b6777851c8b3f96897b72224c40cc3c03019
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565142"
---
# <a name="kspropertycrossbarcanroute"></a>KSPROPERTY\_CROSSBAR\_CAN\_ROUTE


KSPROPERTY\_纵横制\_可以\_路由属性检索设备是否能够支持指定的路由。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_can_route_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_CAN_ROUTE_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p>Filter</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565128" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565128)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定流式处理的微型驱动程序是否支持两个 pin 之间指定路由的 ULONG。 一个非零值指示支持路由。 如果微型驱动程序不支持两个插针之间的路由，此值为零。

<a name="remarks"></a>备注
-------

**CanRoute** KSPROPERTY 成员\_纵横制\_路由\_S 结构指示设备是否能够支持指定的路由。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CROSSBAR\_ROUTE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565128)

 

 






