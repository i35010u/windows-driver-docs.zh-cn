---
title: KSPROPERTY\_BDA\_模板\_连接
description: 客户端使用 KSPROPERTY\_BDA\_模板\_连接检索模板拓扑中的 pin 与节点之间的连接列表。
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
ms.openlocfilehash: e9c24cf3beba8583d376cd187b8840f2263202e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843596"
---
# <a name="ksproperty_bda_template_connections"></a>KSPROPERTY\_BDA\_模板\_连接


客户端使用 KSPROPERTY\_BDA\_模板\_连接检索模板拓扑中的 pin 与节点之间的连接列表。

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
<td><p>BDA_TEMPLATE_CONNECTION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的 BDA\_模板\_连接结构描述模板拓扑中的连接。

模板拓扑中的 pin 与节点之间的连接列表是一组 BDA\_模板\_连接结构。

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


[**BdaPropertyTemplateConnections**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertytemplateconnections)

[**BDA\_模板\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






