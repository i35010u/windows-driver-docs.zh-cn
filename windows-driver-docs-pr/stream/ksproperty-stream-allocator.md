---
title: KSPROPERTY\_流\_分配器
description: KSPROPERTY\_流\_分配器属性是可选属性，如果 pin 分配流缓冲区，或者可以提供一个分配器应实现
ms.assetid: 9a13efe6-4ad4-49bc-b9f1-10c22b47d9d0
keywords:
- KSPROPERTY_STREAM_ALLOCATOR 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_ALLOCATOR
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d720349855711e149387112f4503ff8f025a1042
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526138"
---
# <a name="kspropertystreamallocator"></a>KSPROPERTY\_流\_分配器


KSPROPERTY\_流\_分配器属性是可选属性，如果 pin 分配流缓冲区，或者可以提供一个分配器应实现

## <span id="ddk_ksproperty_stream_allocator_ks"></span><span id="DDK_KSPROPERTY_STREAM_ALLOCATOR_KS"></span>


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
<td><p>句柄</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值始终是**NULL**处理。 但是，支持取决于调用是否成功返回。

该属性设置分配给流连接点的分配器的句柄。 KSPIN 的连接点\_通信\_源检查属性，以确定应使用的数据分配的分配器的句柄。 此属性通常由如 DirectShow 的图形管理器设置。

分配器句柄获得，并可以用于设置另一个筛选器固定的分配器。 使用分配器的筛选器必须引用要获取的文件对象的指针和分配新的分配器时或当连接关闭时取消引用的文件对象的对象。 此外可以查询属性以确定此连接点是否支持提供分配器。

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

 

 






