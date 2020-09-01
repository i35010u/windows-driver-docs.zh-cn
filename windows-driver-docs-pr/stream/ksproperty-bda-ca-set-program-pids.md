---
title: KSPROPERTY \_ BDA \_ CA \_ SET \_ PROGRAM \_ PID
description: 客户端使用 KSPROPERTY \_ BDA \_ CA \_ set \_ PROGRAM \_ pid 在特定程序中设置数据包标识符的列表。
ms.assetid: 5cc049f7-df97-4739-8ec4-22ab646781a6
keywords:
- KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee49a6260e59a93da18e1cec5db8bcd16035f6e2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191785"
---
# <a name="ksproperty_bda_ca_set_program_pids"></a>KSPROPERTY \_ BDA \_ CA \_ SET \_ PROGRAM \_ PID


客户端使用 KSPROPERTY \_ BDA \_ CA \_ set \_ PROGRAM \_ pid 在特定程序中设置数据包标识符的列表。

## <span id="ddk_ksproperty_bda_ca_set_program_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS_KS"></span>


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
<td><p>BDA_PROGRAM_PID_LIST</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BDA \_ PROGRAM \_ PID \_ 列表结构包含指定程序的数据包标识符的列表。

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


[**BDA \_ 程序 \_ PID \_ 列表**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_program_pid_list)

[**KSEVENT \_ BDA \_ 程序 \_ 流 \_ 状态 \_ 已更改**](ksevent-bda-program-flow-status-changed.md)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

