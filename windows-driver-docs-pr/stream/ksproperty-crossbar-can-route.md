---
title: KSPROPERTY\_纵横比\_可以\_路线
description: KSPROPERTY\_纵横制\_可以\_ROUTE 属性检索设备是否能够支持指定的路由。 必须实现此属性。
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
ms.openlocfilehash: 5bb31cb48292da6a950a532cebd0add3579741eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826775"
---
# <a name="ksproperty_crossbar_can_route"></a>KSPROPERTY\_纵横比\_可以\_路线


KSPROPERTY\_纵横制\_可以\_ROUTE 属性检索设备是否能够支持指定的路由。 必须实现此属性。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，指定流式处理微型驱动程序是否支持两个 pin 之间的指定路由。 非零值表示支持路由。 如果微型驱动程序不支持两个插针之间的路由，则此值为零。

<a name="remarks"></a>备注
-------

KSPROPERTY\_\_**纵横比的成员\_** S 结构指示设备是否能够支持指定的路由。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_纵横比\_布线\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)

 

 






