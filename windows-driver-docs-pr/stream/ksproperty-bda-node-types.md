---
title: KSPROPERTY \_ BDA \_ 节点 \_ 类型
description: 客户端使用 KSPROPERTY \_ BDA \_ 节点 \_ 类型来检索节点类型的列表。
ms.assetid: 8fe72434-3635-4c2c-a72a-1fd398e488d8
keywords:
- KSPROPERTY_BDA_NODE_TYPES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_TYPES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb189f49541cefd5635690f384964c1dd2334410
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191109"
---
# <a name="ksproperty_bda_node_types"></a>KSPROPERTY \_ BDA \_ 节点 \_ 类型


客户端使用 KSPROPERTY \_ BDA \_ 节点 \_ 类型来检索节点类型的列表。

## <span id="ddk_ksproperty_bda_node_types_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_TYPES_KS"></span>


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
<td><p>KSNODE_DESCRIPTORs 列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在模板拓扑中，每个节点类型只能出现一次，但它可以在实际拓扑中出现多次。 此节点类型列表是 KSNODE 描述符结构的数组 \_ 。 通常，此数组中每个元素的索引用于标识每个特定节点类型。

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

## <a name="see-also"></a>另请参阅


[**BdaPropertyNodeTypes**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodetypes)

[**KSNODE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

