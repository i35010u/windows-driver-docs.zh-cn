---
title: KSPROPERTY \_ BDA \_ 内 \_ FEC \_ 类型
description: 客户端使用 KSPROPERTY \_ BDA \_ inner \_ FEC \_ 类型来控制内部正向纠错 (FEC) 类型的解调器节点。
keywords:
- KSPROPERTY_BDA_INNER_FEC_TYPE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_INNER_FEC_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa16f099d6289cd3c283aabf8167342a7c66466
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828381"
---
# <a name="ksproperty_bda_inner_fec_type"></a>KSPROPERTY \_ BDA \_ 内 \_ FEC \_ 类型


客户端使用 KSPROPERTY \_ BDA \_ inner \_ FEC \_ 类型来控制内部正向纠错 (FEC) 类型的解调器节点。

## <span id="ddk_ksproperty_bda_inner_fec_type_ks"></span><span id="DDK_KSPROPERTY_BDA_INNER_FEC_TYPE_KS"></span>


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
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p>FECMethod</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

FECMethod 枚举类型返回的值标识 FEC 类型。

KSP **NodeId** \_ 节点的节点标识号指定了解调器节点的标识符。

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


[**FECMethod**](/previous-versions/windows/desktop/mstv/fecmethod)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

