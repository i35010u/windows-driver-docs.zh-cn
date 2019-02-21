---
title: KSPROPERTY\_流\_下降
description: KSPROPERTY\_流\_下降属性是可选属性，如果 pin 允许下降策略应实现。
ms.assetid: b8f9db81-a9ed-4a13-8d64-14854193c91b
keywords:
- KSPROPERTY_STREAM_DEGRADATION 流式处理媒体设备
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
ms.openlocfilehash: 40350124803ca03d65941b025d3d994a0a8a7c25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534802"
---
# <a name="kspropertystreamdegradation"></a>KSPROPERTY\_流\_下降


KSPROPERTY\_流\_下降属性是可选属性，如果 pin 允许下降策略应实现。

## <span id="ddk_ksproperty_stream_degradation_ks"></span><span id="DDK_KSPROPERTY_STREAM_DEGRADATION_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff561671" data-raw-source="[&lt;strong&gt;KSDEGRADE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561671)"> <strong>KSDEGRADE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

查询时，该属性返回的大小和结构中返回的计数[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)格式后, 跟[ **KSDEGRADE**](https://msdn.microsoft.com/library/windows/hardware/ff561671)结构。

上一个查询，此属性返回的大小和计数的结构中 KSMULTIPLE 返回\_项格式后, 跟 KSDEGRADE 结构。 必须在查询和设置下降策略上使用多个项格式。

客户端可以查询此属性来检索当前的下降设置或者它可以设置要更改当前的下降设置此属性。 若要通过筛选器 pin 的质量管理 (QM) 投诉，响应中修改资源的使用情况或调整回一些更高级别的质量使用降级设置。 这通常可供质量管理器来调整下降设置和查询进行调整的设置及其当前值的类型。 设置值时，它可能通过多个 KSDEGRADE 结构。 关于质量管理器的详细信息，请参阅[质量管理](https://msdn.microsoft.com/library/windows/hardware/ff568124)。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDEGRADE**](https://msdn.microsoft.com/library/windows/hardware/ff561671)

 

 






