---
title: KSPROPERTY\_BDA\_NODE\_属性
description: 客户端使用 KSPROPERTY\_BDA\_NODE\_属性来检索节点上支持的属性列表。
ms.assetid: 36d37844-a69b-4f67-bb8f-e5445ba9a2cb
keywords:
- KSPROPERTY_BDA_NODE_PROPERTIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_PROPERTIES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf66aff787a4952b0704a8fa999a687da3c0e2d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844346"
---
# <a name="ksproperty_bda_node_properties"></a>KSPROPERTY\_BDA\_NODE\_属性


客户端使用 KSPROPERTY\_BDA\_NODE\_属性来检索节点上支持的属性列表。

## <span id="ddk_ksproperty_bda_node_properties_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_PROPERTIES_KS"></span>


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
<td><p>KSPROPERTY</p></td>
<td><p>Guid 列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

节点支持的属性列表是 Guid 列表。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaPropertyNodeProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodeproperties)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






