---
title: KSPROPERTY \_ BDA \_ OUTER \_ FEC \_ RATE
description: 客户端使用 KSPROPERTY \_ BDA \_ outer \_ FEC \_ 速率来控制用于外部正向纠错的二进制卷积方案 (FEC) 类型的解调器节点。
keywords:
- KSPROPERTY_BDA_OUTER_FEC_RATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_OUTER_FEC_RATE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60cbd00a2f23ff08376a9d4df786cc9e0ef1fc61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820454"
---
# <a name="ksproperty_bda_outer_fec_rate"></a>KSPROPERTY \_ BDA \_ OUTER \_ FEC \_ RATE


客户端使用 KSPROPERTY \_ BDA \_ outer \_ FEC \_ 速率来控制用于外部正向纠错的二进制卷积方案 (FEC) 类型的解调器节点。

## <span id="ddk_ksproperty_bda_outer_fec_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_OUTER_FEC_RATE_KS"></span>


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
<td><p>BinaryConvolutionCodeRate</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BinaryConvolutionCodeRate 枚举类型返回的值标识二进制卷积方案。

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


[**BinaryConvolutionCodeRate**](/previous-versions/windows/desktop/mstv/binaryconvolutioncoderate)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

