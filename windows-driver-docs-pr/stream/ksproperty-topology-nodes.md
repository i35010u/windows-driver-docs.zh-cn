---
title: KSPROPERTY\_拓扑\_节点
description: KSPROPERTY\_拓扑\_节点提供了一系列的拓扑节点和节点类型支持的筛选器的 Guid。
ms.assetid: 3b07b4d5-b222-44f1-be62-3addf3a87847
keywords:
- KSPROPERTY_TOPOLOGY_NODES 流式处理媒体设备
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
ms.openlocfilehash: bd4a3e8468d9b22db56da3f75484c50143652d01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384146"
---
# <a name="kspropertytopologynodes"></a>KSPROPERTY\_拓扑\_节点


KSPROPERTY\_拓扑\_节点提供了一系列的拓扑节点和节点类型支持的筛选器的 Guid。

## <span id="ddk_ksproperty_topology_nodes_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_NODES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>结构后, 跟一系列 Guid。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

GUID 列表表示节点类型。 在序列内的索引必须与匹配的节点 ID 号。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

 

 






