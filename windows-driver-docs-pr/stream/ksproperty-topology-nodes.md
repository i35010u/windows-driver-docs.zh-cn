---
title: KSPROPERTY \_ 拓扑 \_ 节点
description: KSPROPERTY \_ 拓扑 \_ 节点提供筛选器支持的拓扑节点和节点类型 guid 的列表。
ms.assetid: 3b07b4d5-b222-44f1-be62-3addf3a87847
keywords:
- KSPROPERTY_TOPOLOGY_NODES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_NODES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26c675972bbe45c6ad73e2baf77d46e50f6fa9c3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103370"
---
# <a name="ksproperty_topology_nodes"></a>KSPROPERTY \_ 拓扑 \_ 节点


KSPROPERTY \_ 拓扑 \_ 节点提供筛选器支持的拓扑节点和节点类型 guid 的列表。

## <span id="ddk_ksproperty_topology_nodes_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_NODES_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列 guid。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

GUID 列表表示节点类型。 序列内的索引必须与节点 ID 号相匹配。

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

