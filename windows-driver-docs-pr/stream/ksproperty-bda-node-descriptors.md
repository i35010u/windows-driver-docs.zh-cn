---
title: KSPROPERTY \_ BDA \_ 节点 \_ 描述符
description: 客户端使用 KSPROPERTY \_ BDA \_ 节点 \_ 描述符来检索节点列表。
keywords:
- KSPROPERTY_BDA_NODE_DESCRIPTORS 流媒体设备
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
ms.openlocfilehash: 34232426dbbe7cea0245f748a070a700c4ee7e70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840259"
---
# <a name="ksproperty_bda_node_descriptors"></a>KSPROPERTY \_ BDA \_ 节点 \_ 描述符


客户端使用 KSPROPERTY \_ BDA \_ 节点 \_ 描述符来检索节点列表。

## <span id="ddk_ksproperty_bda_node_descriptors_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_DESCRIPTORS_KS"></span>


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
<td><p>KSPROPERTY</p></td>
<td><p>Guid 列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

节点列表是可用节点的 Guid 数组。

有关可在模板拓扑中创建的 BDA 节点的列表，请参阅 [Bda 节点类别 guid](bda-node-category-guids.md)。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BdaPropertyNodeDescriptors**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodedescriptors)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

