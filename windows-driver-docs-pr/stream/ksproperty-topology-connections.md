---
title: KSPROPERTY\_拓扑\_连接
description: KSPROPERTY\_拓扑\_连接属性查询 KS 筛选器节点之间的所有连接。
ms.assetid: 8ea77244-14c1-4e27-9b96-e0f5a6c491e9
keywords:
- KSPROPERTY_TOPOLOGY_CONNECTIONS 流媒体设备
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
ms.openlocfilehash: b2aacbf495426f3bbac04e3e40d39e1b931ea022
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837926"
---
# <a name="ksproperty_topology_connections"></a>KSPROPERTY\_拓扑\_连接


KSPROPERTY\_拓扑\_连接属性查询 KS 筛选器节点之间的所有连接。

## <span id="ddk_ksproperty_topology_connections_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_CONNECTIONS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_CONNECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)"><strong>KSTOPOLOGY_CONNECTION</strong></a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSMULTIPLE\_项标头后跟 KSTOPOLOGY\_连接结构，该结构描述了 KS 筛选器中的单个数据路径连接。

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

[**KSTOPOLOGY\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)

 

 






