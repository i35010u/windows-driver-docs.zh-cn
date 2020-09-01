---
title: KSPROPERTY \_ BDA \_ PIDFILTER 取消 \_ 映射 \_ PID
description: 客户端使用 KSPROPERTY \_ BDA PIDFILTER 取消标记 \_ \_ \_ 来通知 PID 筛选器节点有关使用特定 pid 标识的数据包，以便从输入流进行筛选 (即，停止从输入传递到输出) 。
ms.assetid: 111d8857-84f4-4a7f-8771-ea6537c4c592
keywords:
- KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4af19e3a06972627aa1e74eddf43cb7fd90857c1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192157"
---
# <a name="ksproperty_bda_pidfilter_unmap_pids"></a>KSPROPERTY \_ BDA \_ PIDFILTER 取消 \_ 映射 \_ PID


客户端使用 KSPROPERTY \_ BDA PIDFILTER 取消标记 \_ \_ \_ 来通知 PID 筛选器节点有关使用特定 pid 标识的数据包，以便从输入流进行筛选 (即，停止从输入传递到输出) 。

## <span id="ddk_ksproperty_bda_pidfilter_unmap_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS_KS"></span>


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
<td><p>BDA_PID_UNMAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点标识号指定 PID 筛选器节点的标识符。

BDA \_ PID 取消 \_ 结构描述了使用特定 pid 标识的数据包映射，以从输入流进行筛选。

此列表中不是由节点传递的任何 PID 都将被忽略。

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


[**BDA \_ PID 取消 \_ 映射**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_pid_unmap)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

