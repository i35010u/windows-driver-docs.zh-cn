---
title: KSPROPERTY \_ 横线 \_ 路由
description: KSPROPERTY \_ 纵横制 \_ 路由属性用于查询是否可以进行特定的路由，以及如何通过指定输出 pin 索引和输入 pin 索引来路由视频或音频流。 必须实现此属性。
keywords:
- KSPROPERTY_CROSSBAR_ROUTE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_ROUTE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7a2bc3011a22e0afcb6df4a6616d0221e4a5de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837619"
---
# <a name="ksproperty_crossbar_route"></a>KSPROPERTY \_ 横线 \_ 路由


KSPROPERTY \_ 纵横制 \_ 路由属性用于查询是否可以进行特定的路由，以及如何通过指定输出 pin 索引和输入 pin 索引来路由视频或音频流。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_route_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_ROUTE_KS"></span>


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
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ 交叉 \_ 路由 \_ 结构，它指定特定的路由，以及该路由是否可以。

<a name="remarks"></a>备注
-------

当路由到的输入插针索引为-1 时，音频输出插针应该为输出音频流静音，如更改通道时。

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ 横线 \_ 路由 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_route_s)

