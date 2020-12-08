---
title: KSPROPERTY \_ BDA \_ 模板 \_ 连接
description: 客户端使用 KSPROPERTY \_ BDA \_ 模板 \_ 连接来检索模板拓扑中的 pin 与节点之间的连接列表。
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
ms.openlocfilehash: c1dd2c6fdb631b7ea224dc0e3465f0a31b96a4fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804357"
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

## <a name="see-also"></a>请参阅


[**BdaPropertyTemplateConnections**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertytemplateconnections)

[**BDA \_ 模板 \_ 连接**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

