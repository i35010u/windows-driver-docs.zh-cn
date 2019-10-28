---
title: KSPROPERTY\_拓扑\_节点
description: KSPROPERTY\_拓扑\_节点提供筛选器支持的拓扑节点和节点类型 Guid 的列表。
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
ms.openlocfilehash: 9a25eb5ba048c5399880c8df1f07ce326b8a41b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837921"
---
# <a name="ksproperty_topology_nodes"></a>KSPROPERTY\_拓扑\_节点


KSPROPERTY\_拓扑\_节点提供筛选器支持的拓扑节点和节点类型 Guid 的列表。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列 guid。</p></td>
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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






