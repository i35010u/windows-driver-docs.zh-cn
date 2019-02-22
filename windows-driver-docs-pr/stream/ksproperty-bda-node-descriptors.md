---
title: KSPROPERTY\_BDA\_节点\_描述符
description: 客户端使用 KSPROPERTY\_BDA\_节点\_描述符来检索节点的列表。
ms.assetid: 53b297e6-7e31-4231-80ad-b114cf9343b4
keywords:
- KSPROPERTY_BDA_NODE_DESCRIPTORS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_DESCRIPTORS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9bdad8f5fc1bab91f02a31257506e81dc9d1cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542446"
---
# <a name="kspropertybdanodedescriptors"></a>KSPROPERTY\_BDA\_节点\_描述符


客户端使用 KSPROPERTY\_BDA\_节点\_描述符来检索节点的列表。

## <span id="ddk_ksproperty_bda_node_descriptors_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_DESCRIPTORS_KS"></span>


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
<td><p>KSPROPERTY</p></td>
<td><p>Guid 的列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

节点列表是可用节点的 Guid 的数组。

有关可用于在模板拓扑中创建的 BDA 节点的列表，请参阅[BDA 节点类别 Guid](bda-node-category-guids.md)。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaPropertyNodeDescriptors**](https://msdn.microsoft.com/library/windows/hardware/ff556484)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






