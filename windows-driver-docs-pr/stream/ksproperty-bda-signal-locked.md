---
title: 已 \_ 锁定 KSPROPERTY BDA \_ 信号 \_
description: 客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 进行锁定，以确定是否可以锁定信号。
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCKED 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCKED
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38726772d776c7fa750232ec0c4ca04ceca08143
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828377"
---
# <a name="ksproperty_bda_signal_locked"></a>已 \_ 锁定 KSPROPERTY BDA \_ 信号 \_


客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 进行锁定，以确定是否可以锁定信号。

## <span id="ddk_ksproperty_bda_signal_locked_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_LOCKED_KS"></span>


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
<td><p>固定或筛选</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点1指定了控制节点的标识符，或设置为−1以指定 pin。

返回的值指示是否可以锁定信号。 如果信号可以锁定， **则返回 TRUE** ，否则返回 **FALSE** 。

如果 RF 调谐器节点返回 **TRUE**，则通常会指示 (PLL) 锁定的阶段锁循环。

如果某个解调器节点返回 **TRUE**，则指示至少有20% 的信号质量。

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


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSPROPERTY \_ BDA \_ 信号 \_ 质量**](ksproperty-bda-signal-quality.md)

 

