---
title: KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 极性
description: 客户端使用 KSPROPERTY \_ BDA \_ RF RF \_ \_ 极性来控制调谐器节点的极性设置。
ms.assetid: 6778b4ac-2444-4e27-ab80-5802dda09fdd
keywords:
- KSPROPERTY_BDA_RF_TUNER_POLARITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_POLARITY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a585454d45bd8bc76ff973eb566574de842a9af
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187105"
---
# <a name="ksproperty_bda_rf_tuner_polarity"></a>KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 极性


客户端使用 KSPROPERTY \_ BDA \_ RF RF \_ \_ 极性来控制调谐器节点的极性设置。

## <span id="ddk_ksproperty_bda_rf_tuner_polarity_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_POLARITY_KS"></span>


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

 

<a name="remarks"></a>注解
-------

KSP **NodeId** \_ 节点的节点标识号指定调谐器节点的标识符。

属性值指定为传输的信号设置的极性。

对于某些传输，特别是卫星传输，信号可能会很有出入。 此属性告知调谐器节点有关传输的信号的 polarization。 Polarization 枚举类型包含指定信号极性的值。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**Polarization**](/previous-versions/windows/hardware/drivers/ff567780(v=vs.85))

 

