---
title: KSPROPERTY \_ BDA \_ 节点 \_ 方法
description: 客户端使用 KSPROPERTY \_ BDA \_ 节点 \_ 方法检索节点上支持的方法的列表。
keywords:
- KSPROPERTY_BDA_NODE_METHODS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_METHODS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b473be01241cab7efb08ee7d7f808539d5854842
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840255"
---
# <a name="ksproperty_bda_node_methods"></a>KSPROPERTY \_ BDA \_ 节点 \_ 方法


客户端使用 KSPROPERTY \_ BDA \_ 节点 \_ 方法检索节点上支持的方法的列表。

## <span id="ddk_ksproperty_bda_node_methods_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_METHODS_KS"></span>


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

节点支持的方法列表是 Guid 列表。

网络提供商将使用此属性来查询 BDA 模板连接列表中每个节点的功能。

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


[**BdaPropertyNodeMethods**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodemethods)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

