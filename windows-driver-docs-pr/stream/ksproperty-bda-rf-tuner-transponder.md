---
title: KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ TRANSPONDER
description: 客户端使用 KSPROPERTY \_ BDA \_ RF \_ 调谐器 TRANSPONDER 将 \_ 相应 TRANSPONDER 号码的调谐器节点通知给调谐器节点。
ms.assetid: 00445260-a317-4341-baab-d1391f6748e4
keywords:
- KSPROPERTY_BDA_RF_TUNER_TRANSPONDER 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_TRANSPONDER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab26a4f1760fa3b64eadfb1a1f4f6225cc746d8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190175"
---
# <a name="ksproperty_bda_rf_tuner_transponder"></a>KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ TRANSPONDER


客户端使用 KSPROPERTY \_ BDA \_ RF \_ 调谐器 TRANSPONDER 将 \_ 相应 TRANSPONDER 号码的调谐器节点通知给调谐器节点。

## <span id="ddk_ksproperty_bda_rf_tuner_transponder_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_TRANSPONDER_KS"></span>


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

KSP **NodeId** \_ 节点的节点标识号指定调谐器节点的标识符。

属性值指定要设置的 transponder 数字。

某些优化空间包含了有关如何获取嵌入在硬件中的频率的所有信息。 这些微调空间指定了 transponder 的数字。 此属性通知此 transponder 数字的调谐器节点。 然后，调谐器硬件可以自动确定获取中间频率所需的优化特性。 在这种情况下，KSPROPSETID BdaFrequencyFilter 属性集中的其他属性设置 \_ 为−1。

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


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

