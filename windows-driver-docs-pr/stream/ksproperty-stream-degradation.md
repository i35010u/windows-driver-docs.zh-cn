---
title: KSPROPERTY \_ 流 \_ 降级
description: KSPROPERTY \_ 流 \_ 降级属性是一个可选属性，如果 pin 允许降级策略，则应实现该属性。
ms.assetid: b8f9db81-a9ed-4a13-8d64-14854193c91b
keywords:
- KSPROPERTY_STREAM_DEGRADATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_DEGRADATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7445bb59930e6478fe6e4a71f38472fcee9c64a8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103032"
---
# <a name="ksproperty_stream_degradation"></a>KSPROPERTY \_ 流 \_ 降级


KSPROPERTY \_ 流 \_ 降级属性是一个可选属性，如果 pin 允许降级策略，则应实现该属性。

## <span id="ddk_ksproperty_stream_degradation_ks"></span><span id="DDK_KSPROPERTY_STREAM_DEGRADATION_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>， <a href="/previous-versions/ff561671(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDEGRADE&lt;/strong&gt;](/previous-versions/ff561671(v=vs.85))"> <strong>KSDEGRADE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

查询时，属性返回要以 [**KSMULTIPLE \_ ITEM**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item) 格式返回的结构的大小和计数，后跟 [**KSDEGRADE**](/previous-versions/ff561671(v=vs.85)) 结构。

在查询中，此属性返回要以 KSMULTIPLE ITEM 格式返回的结构的大小和计数 \_ ，后跟 KSDEGRADE 结构。 在查询和设置降级策略时，必须使用多项格式。

客户端可以查询此属性以检索当前的降级设置，也可以设置此属性来更改当前的降级设置。 降级设置用于通过筛选器 pin 来修改资源的使用情况，以响应质量管理 (QM) 投诉，或将质量调整回更高的级别。 这通常由质量管理器用来调整降级设置，并查询可调整的设置类型及其当前值。 设置值时，它可能传递多个 KSDEGRADE 结构。 有关质量管理器的详细信息，请参阅 [质量管理](./quality-management.md)。

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


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDEGRADE**](/previous-versions/ff561671(v=vs.85))

