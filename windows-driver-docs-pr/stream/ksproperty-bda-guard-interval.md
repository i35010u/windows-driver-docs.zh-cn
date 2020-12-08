---
title: KSPROPERTY \_ BDA \_ GUARD \_ 间隔
description: 客户端使用 KSPROPERTY \_ BDA \_ GUARD \_ 间隔来控制某个解调器节点的临界间隔设置。
keywords:
- KSPROPERTY_BDA_GUARD_INTERVAL 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_GUARD_INTERVAL
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba96d0279c613b4eaf408472bc12a6000285bc44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824937"
---
# <a name="ksproperty_bda_guard_interval"></a>KSPROPERTY \_ BDA \_ GUARD \_ 间隔


客户端使用 KSPROPERTY \_ BDA \_ GUARD \_ 间隔来控制某个解调器节点的临界间隔设置。

## <span id="ddk_ksproperty_bda_guard_interval_ks"></span><span id="DDK_KSPROPERTY_BDA_GUARD_INTERVAL_KS"></span>


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
<td><p>GuardInterval</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

GuardInterval 枚举类型的返回值标识临界间隔的设置。

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


[**GuardInterval**](/previous-versions/windows/desktop/mstv/guardinterval)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

