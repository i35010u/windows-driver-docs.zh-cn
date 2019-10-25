---
title: KSPROPERTY\_BDA\_NODE\_方法
description: 客户端\_BDA\_NODE\_方法使用 KSPROPERTY 来检索节点上支持的方法的列表。
ms.assetid: 143456dc-1910-4db4-8584-9cd19d09e8ce
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
ms.openlocfilehash: 2322cc7ead722b427a3233dca290c1dc180a8b67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844347"
---
# <a name="ksproperty_bda_node_methods"></a>KSPROPERTY\_BDA\_NODE\_方法


客户端\_BDA\_NODE\_方法使用 KSPROPERTY 来检索节点上支持的方法的列表。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaPropertyNodeMethods**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodemethods)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






