---
title: KSPROPERTY\_BDA\_RF\_调谐器\_TRANSPONDER
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_TRANSPONDER 将相应 TRANSPONDER 号码的调谐器节点通知给调谐器节点。
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
ms.openlocfilehash: 01e97e0544dfd6907e929b3dafbdc97dfe2a3e89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838079"
---
# <a name="ksproperty_bda_rf_tuner_transponder"></a>KSPROPERTY\_BDA\_RF\_调谐器\_TRANSPONDER


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_TRANSPONDER 将相应 TRANSPONDER 号码的调谐器节点通知给调谐器节点。

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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识符指定调谐器节点的标识符。

属性值指定要设置的 transponder 数字。

某些优化空间包含了有关如何获取嵌入在硬件中的频率的所有信息。 这些微调空间指定了 transponder 的数字。 此属性通知此 transponder 数字的调谐器节点。 然后，调谐器硬件可以自动确定获取中间频率所需的优化特性。 在这种情况下，KSPROPSETID\_BdaFrequencyFilter 属性集中的其他属性设置为−1。

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


[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






