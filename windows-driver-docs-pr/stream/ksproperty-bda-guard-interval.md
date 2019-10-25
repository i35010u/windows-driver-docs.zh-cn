---
title: KSPROPERTY\_BDA\_GUARD\_间隔
description: 客户端使用 KSPROPERTY\_BDA\_GUARD\_间隔来控制某个解调器节点的临界间隔设置。
ms.assetid: 7c0c6c5e-94fd-4013-9778-d41568ae9f0b
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
ms.openlocfilehash: 18fe020a72eae161a2b2f705b5563fabac75d12f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842143"
---
# <a name="ksproperty_bda_guard_interval"></a>KSPROPERTY\_BDA\_GUARD\_间隔


客户端使用 KSPROPERTY\_BDA\_GUARD\_间隔来控制某个解调器节点的临界间隔设置。

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
<td><p>GuardInterval</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

GuardInterval 枚举类型的返回值标识临界间隔的设置。

KSP\_**节点的节点**标识号指定了解调器节点的标识符。

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


[**GuardInterval**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/guardinterval)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






