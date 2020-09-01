---
title: KSPROPERTY \_ BDA \_ 模板 \_ 连接
description: 客户端使用 KSPROPERTY \_ BDA \_ 模板 \_ 连接来检索模板拓扑中的 pin 与节点之间的连接列表。
ms.assetid: 59268751-34fd-4291-bf36-45a435a4ccf2
keywords:
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b42fb47f9426bd2863a142b733ff0ef72679512
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193011"
---
# <a name="ksproperty_bda_template_connections"></a>KSPROPERTY \_ BDA \_ 模板 \_ 连接


客户端使用 KSPROPERTY \_ BDA \_ 模板 \_ 连接来检索模板拓扑中的 pin 与节点之间的连接列表。

## <span id="ddk_ksproperty_bda_template_connections_ks"></span><span id="DDK_KSPROPERTY_BDA_TEMPLATE_CONNECTIONS_KS"></span>


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
<td><p>BDA_TEMPLATE_CONNECTION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的 BDA \_ 模板 \_ 连接结构描述了模板拓扑中的连接。

模板拓扑中的 pin 与节点之间的连接列表是一组 BDA \_ 模板 \_ 连接结构。

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


[**BdaPropertyTemplateConnections**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertytemplateconnections)

[**BDA \_ 模板 \_ 连接**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

