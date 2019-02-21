---
title: KSPROPERTY\_拓扑\_连接
description: KSPROPERTY\_拓扑\_连接属性查询 KS 筛选器的节点之间的所有连接。
ms.assetid: 8ea77244-14c1-4e27-9b96-e0f5a6c491e9
keywords:
- KSPROPERTY_TOPOLOGY_CONNECTIONS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_CONNECTIONS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 672feb6cfe9fa9b514958f978bb6069375168d74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534801"
---
# <a name="kspropertytopologyconnections"></a>KSPROPERTY\_拓扑\_连接


KSPROPERTY\_拓扑\_连接属性查询 KS 筛选器的节点之间的所有连接。

## <span id="ddk_ksproperty_topology_connections_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_CONNECTIONS_KS"></span>


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
<td><p>一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>结构后, 跟一系列<a href="https://msdn.microsoft.com/library/windows/hardware/ff567148" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_CONNECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567148)"> <strong>KSTOPOLOGY_CONNECTION</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSMULTIPLE\_项标头后跟 KSTOPOLOGY\_连接结构，它描述 KS 筛选器中的单个数据路径连接。

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

[**KSTOPOLOGY\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff567148)

 

 






