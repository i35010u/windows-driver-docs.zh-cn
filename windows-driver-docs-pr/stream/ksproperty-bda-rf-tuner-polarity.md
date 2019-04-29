---
title: KSPROPERTY\_BDA\_RF\_调谐器\_极性
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_极性来控制调谐器节点的极性设置。
ms.assetid: 6778b4ac-2444-4e27-ab80-5802dda09fdd
keywords:
- KSPROPERTY_BDA_RF_TUNER_POLARITY 流式处理媒体设备
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
ms.openlocfilehash: edc0960b74e48a1d4428250ed87754950a8a1d37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389313"
---
# <a name="kspropertybdarftunerpolarity"></a>KSPROPERTY\_BDA\_RF\_调谐器\_极性


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_极性来控制调谐器节点的极性设置。

## <span id="ddk_ksproperty_bda_rf_tuner_polarity_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_POLARITY_KS"></span>


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
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定调谐器节点的标识符。

属性值指定为传输信号设置极性。

某些传输，尤其是卫星传输，可能极化信号。 此属性告知极化传输信号的调谐器节点。 极化枚举类型包含指定的信号的极性的值。

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


[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

[**极化**](https://msdn.microsoft.com/library/windows/hardware/ff567780)

 

 






