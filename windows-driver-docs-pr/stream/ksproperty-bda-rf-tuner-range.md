---
title: KSPROPERTY\_BDA\_RF\_调谐器\_范围
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_范围控制调谐器范围，即，查找特定载波频率的域。
ms.assetid: 2f2aa515-3f3c-419f-a817-0d597466ec85
keywords:
- KSPROPERTY_BDA_RF_TUNER_RANGE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_RANGE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70aeaee6522dfa336b210bb856d088aec1c92837
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838073"
---
# <a name="ksproperty_bda_rf_tuner_range"></a>KSPROPERTY\_BDA\_RF\_调谐器\_范围


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_范围控制调谐器范围，即，查找特定载波频率的域。

## <span id="ddk_ksproperty_bda_rf_tuner_range_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_RANGE_KS"></span>


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

属性值指定要设置的调谐器范围。

通过以下方式指定 KSPROPERTY\_BDA\_RF\_调谐器\_范围属性：

-   BDA\_范围\_不\_集（−1）指示未设置调谐器范围。

-   BDA\_范围\_未定义\_（0）指示未定义调谐器范围。

某些调谐器控制外部设备（例如 multiswitch），用于定义要在其上查找特定载波频率的域。 此属性将调谐器范围设置为−1，这意味着调谐器范围不用于特定的优化空间，或设置为特定于优化空间的值。

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

 

 






