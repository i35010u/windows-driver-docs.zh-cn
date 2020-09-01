---
title: KSPROPERTY \_ BDA \_ 符号 \_ 速率
description: 客户端使用 KSPROPERTY \_ BDA \_ 符号 \_ 速率来控制某个解调器节点的符号速率。
ms.assetid: 11e2e020-3037-4a68-a8d6-c68efd86a518
keywords:
- KSPROPERTY_BDA_SYMBOL_RATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SYMBOL_RATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66a0f81309b96e4fa26da1f4ea780b284af69ff1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192401"
---
# <a name="ksproperty_bda_symbol_rate"></a>KSPROPERTY \_ BDA \_ 符号 \_ 速率


客户端使用 KSPROPERTY \_ BDA \_ 符号 \_ 速率来控制某个解调器节点的符号速率。

## <span id="ddk_ksproperty_bda_symbol_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_SYMBOL_RATE_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定符号速率。

KSP **NodeId** \_ 节点的节点标识号指定了解调器节点的标识符。

## <a name="see-also"></a>另请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

