---
title: KSPROPERTY\_BDA\_PIDFILTER\_取消映射\_PID
description: 客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_取消映射\_PID，通知 PID 筛选器节点有关使用特定 Pid 标识的数据包，以便从输入流进行筛选（即，停止从输入传递到输出）。
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
ms.openlocfilehash: 68fa8e43a950b09cdc379c0f473ce8ce6a96b717
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837608"
---
# <a name="ksproperty_bda_pidfilter_unmap_pids"></a>KSPROPERTY\_BDA\_PIDFILTER\_取消映射\_PID


客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_取消映射\_PID，通知 PID 筛选器节点有关使用特定 Pid 标识的数据包，以便从输入流进行筛选（即，停止从输入传递到输出）。

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
<td><p>BDA_PID_UNMAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识指定 PID 筛选器节点的标识符。

BDA\_PID\_取消映射结构描述了使用特定 Pid 标识的数据包映射，以从输入流进行筛选。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BDA\_PID\_取消映射**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_pid_unmap)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






