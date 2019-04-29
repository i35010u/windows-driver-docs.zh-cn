---
title: KSPROPERTY\_BDA\_节点\_事件
description: 客户端使用 KSPROPERTY\_BDA\_节点\_事件，以检索支持的节点上的事件列表。
ms.assetid: 4923a88b-abb3-4608-95b3-b0e74eeadaa8
keywords:
- KSPROPERTY_BDA_NODE_EVENTS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_EVENTS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d44722d9ade9836b1bc5cad629e1453eaa4511
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387933"
---
# <a name="kspropertybdanodeevents"></a>KSPROPERTY\_BDA\_节点\_事件


客户端使用 KSPROPERTY\_BDA\_节点\_事件，以检索支持的节点上的事件列表。

## <span id="ddk_ksproperty_bda_node_events_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_EVENTS_KS"></span>


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

支持一个节点的事件的列表是列表的 Guid。

网络提供商将使用此属性查询 BDA 模板连接列表中每个节点的功能。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BdaPropertyNodeEvents**](https://msdn.microsoft.com/library/windows/hardware/ff556488)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






