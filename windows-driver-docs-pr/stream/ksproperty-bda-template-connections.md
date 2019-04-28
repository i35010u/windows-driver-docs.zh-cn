---
title: KSPROPERTY\_BDA\_模板\_连接
description: 客户端使用 KSPROPERTY\_BDA\_模板\_连接来检索的插针和模板拓扑中的节点之间的连接列表。
ms.assetid: 59268751-34fd-4291-bf36-45a435a4ccf2
keywords:
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS 流式处理媒体设备
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
ms.openlocfilehash: 45e0864fb84b9f86c3be3db8d6c2658134276871
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344961"
---
# <a name="kspropertybdatemplateconnections"></a>KSPROPERTY\_BDA\_模板\_连接


客户端使用 KSPROPERTY\_BDA\_模板\_连接来检索的插针和模板拓扑中的节点之间的连接列表。

## <span id="ddk_ksproperty_bda_template_connections_ks"></span><span id="DDK_KSPROPERTY_BDA_TEMPLATE_CONNECTIONS_KS"></span>


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
<td><p>BDA_TEMPLATE_CONNECTION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的 BDA\_模板\_连接结构描述模板拓扑中的连接。

Pin 和模板拓扑中的节点之间的连接列表是一个数组 BDA\_模板\_连接结构。

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


[**BdaPropertyTemplateConnections**](https://msdn.microsoft.com/library/windows/hardware/ff556501)

[**BDA\_模板\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff556558)

[**KSPIN\_描述符\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






