---
title: KSPROPERTY\_BDA\_INNER\_FEC\_类型
description: 客户端使用 KSPROPERTY\_BDA\_INNER\_FEC\_类型来控制某个解调器节点的内部正向纠错（FEC）类型。
ms.assetid: e6640d89-cf75-4073-98fb-2a877d6c38d3
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
ms.openlocfilehash: 659ef3981d8a2547b4f6b18daecd3006486ab6ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845558"
---
# <a name="ksproperty_bda_inner_fec_type"></a>KSPROPERTY\_BDA\_INNER\_FEC\_类型


客户端使用 KSPROPERTY\_BDA\_INNER\_FEC\_类型来控制某个解调器节点的内部正向纠错（FEC）类型。

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
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>FECMethod</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

FECMethod 枚举类型返回的值标识 FEC 类型。

KSP\_**节点的节点**标识号指定了解调器节点的标识符。

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


[**FECMethod**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/fecmethod)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






