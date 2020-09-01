---
title: KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 范围
description: 客户端使用 KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 范围控制调谐器范围，即，查找特定载波频率的域。
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
ms.openlocfilehash: 3c23c870a4a0da37dfec7e250bf8d879b74c9e40
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191077"
---
# <a name="ksproperty_bda_rf_tuner_range"></a>KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 范围


客户端使用 KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 范围控制调谐器范围，即，查找特定载波频率的域。

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

属性值指定要设置的调谐器范围。

\_ \_ 用以下内容指定 KSPROPERTY BDA RF \_ 调谐器 \_ 范围属性：

-   \_ \_ 未设置 BDA 范围 \_ (− 1) 指示未设置调谐器范围。

-   \_ \_ 未定义 BDA 范围 \_ (0) 指示未定义调谐器范围。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

