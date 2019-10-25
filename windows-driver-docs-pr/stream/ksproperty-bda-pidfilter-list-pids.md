---
title: KSPROPERTY\_BDA\_PIDFILTER\_列表\_PID
description: 客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_LIST\_PID 从 PID 筛选器节点检索用于标识节点从输入流传递到输出流的包的列表。
ms.assetid: fc7dc0af-af74-4bd1-b99c-f06de25aae3c
keywords:
- KSPROPERTY_BDA_PIDFILTER_LIST_PIDS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIDFILTER_LIST_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc7ddeb9eb904fcc5e6ba24c6c5da1cb3d7385d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837614"
---
# <a name="ksproperty_bda_pidfilter_list_pids"></a>KSPROPERTY\_BDA\_PIDFILTER\_列表\_PID


客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_LIST\_PID 从 PID 筛选器节点检索用于标识节点从输入流传递到输出流的包的列表。

## <span id="ddk_ksproperty_bda_pidfilter_list_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_LIST_PIDS_KS"></span>


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
<td><p>Pid 列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识指定 PID 筛选器节点的标识符。

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

 

 






