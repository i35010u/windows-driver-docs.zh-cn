---
title: KSPROPERTY\_拓扑\_名称
description: KSPROPERTY\_拓扑\_NAME 属性提供节点的本地化 Unicode 字符串名称。
ms.assetid: ae12fe2f-9ccf-4949-b530-e7e33c846837
keywords:
- KSPROPERTY_TOPOLOGY_NAME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_NAME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6910f7fe0253dee1d7f99e2eb51b317b6fb2d021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837924"
---
# <a name="ksproperty_topology_name"></a>KSPROPERTY\_拓扑\_名称


KSPROPERTY\_拓扑\_NAME 属性提供节点的本地化 Unicode 字符串名称。

## <span id="ddk_ksproperty_topology_name_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_NAME_KS"></span>


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
<td><p>节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)"><strong>KSP_NODE</strong></a></p></td>
<td><p>用于保存字符串名称的缓冲区。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_节点**结构的节点**ID 指定要为其返回字符串名称的节点 ID。

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


[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






