---
title: KSPROPERTY\_流\_降级
description: KSPROPERTY\_STREAM\_降级属性是一个可选属性，如果 pin 允许降级策略，则应实现该属性。
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
ms.openlocfilehash: cfc104f7b61d032819b75fd434b2128684414b09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844958"
---
# <a name="ksproperty_stream_degradation"></a>KSPROPERTY\_流\_降级


KSPROPERTY\_STREAM\_降级属性是一个可选属性，如果 pin 允许降级策略，则应实现该属性。

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
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>、 <a href="https://docs.microsoft.com/previous-versions/ff561671(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDEGRADE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))"> <strong>KSDEGRADE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

查询时，属性将返回[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)格式返回的结构的大小和计数，后跟[**KSDEGRADE**](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))结构。

在查询中，此属性返回以 KSMULTIPLE\_项格式返回的结构的大小和计数，后跟 KSDEGRADE 结构。 在查询和设置降级策略时，必须使用多项格式。

客户端可以查询此属性以检索当前的降级设置，也可以设置此属性来更改当前的降级设置。 降级设置用于修改筛选器 pin 对质量管理（QM）投诉的资源使用情况，或将质量调整回更高的级别。 这通常由质量管理器用来调整降级设置，并查询可调整的设置类型及其当前值。 设置值时，它可能传递多个 KSDEGRADE 结构。 有关质量管理器的详细信息，请参阅[质量管理](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management)。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDEGRADE**](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))

 

 






