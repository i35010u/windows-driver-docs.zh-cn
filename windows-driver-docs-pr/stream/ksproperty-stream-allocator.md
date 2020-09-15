---
title: KSPROPERTY \_ 流 \_ 分配器
description: KSPROPERTY \_ 流 \_ 分配器属性是一个可选属性，如果 pin 分配流缓冲区或可提供分配器，则应实现此属性
ms.assetid: 9a13efe6-4ad4-49bc-b9f1-10c22b47d9d0
keywords:
- KSPROPERTY_STREAM_ALLOCATOR 流媒体设备
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
ms.openlocfilehash: ade2f8a3d9ffe48b2ea7a8736e7096cf410b6d44
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103036"
---
# <a name="ksproperty_stream_allocator"></a>KSPROPERTY \_ 流 \_ 分配器


KSPROPERTY \_ 流 \_ 分配器属性是一个可选属性，如果 pin 分配流缓冲区或可提供分配器，则应实现此属性

## <span id="ddk_ksproperty_stream_allocator_ks"></span><span id="DDK_KSPROPERTY_STREAM_ALLOCATOR_KS"></span>


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
<td><p>句柄</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

返回的值始终为 **NULL** 句柄。 但是，支持由调用是否成功返回决定。

属性设置分配给流连接点的分配器的句柄。 KSPIN 通信源的连接 \_ 点 \_ 检查属性，以确定应该用于数据分配的分配器的句柄。 此属性通常由图形管理器（如 DirectShow）设置。

获取分配器句柄，并可用于为另一个筛选器 pin 设置分配器。 使用分配器的筛选器必须引用对象，以获取指向文件对象的指针，并在分配新分配器或关闭连接时取消引用文件对象。 还可以查询属性以确定此连接点是否支持提供分配器。

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

