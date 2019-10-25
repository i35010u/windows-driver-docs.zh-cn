---
title: KSPROPERTY\_BDA\_PIDFILTER\_映射\_PID
description: 客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_映射\_PID，通知 PID 筛选器节点有关应传递到下游筛选器或节点的传输流数据包列表。
ms.assetid: 33d2775c-308a-4af0-81ae-b174990926ad
keywords:
- KSPROPERTY_BDA_PIDFILTER_MAP_PIDS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIDFILTER_MAP_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70cf8a8300322e3e642f02ebcbd89b51711f8418
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837612"
---
# <a name="ksproperty_bda_pidfilter_map_pids"></a>KSPROPERTY\_BDA\_PIDFILTER\_映射\_PID


客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_映射\_PID，通知 PID 筛选器节点有关应传递到下游筛选器或节点的传输流数据包列表。 此属性还通知 PID 筛选器节点在该节点的输出上传递数据时要使用的输出类型（例如表节或传输流）。

## <span id="ddk_ksproperty_bda_pidfilter_map_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_MAP_PIDS_KS"></span>


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
<td><p>BDA_PID_MAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识指定 PID 筛选器节点的标识符。

BDA\_PID\_MAP 结构描述了要从输入流中筛选出的数据的映射。

PID 筛选器节点将随此属性提供的列表与节点当前通过下游传递的 Pid 列表合并。 如果提供的列表中的 PID 已经在 PID 筛选器节点的列表中，则提供的列表的输出类型将优先。 此属性还可用于检索节点输出的数据的类型。 BDA\_PID\_MAP 结构描述此输出数据的映射。

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


[**BDA\_PID\_映射**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_pid_map)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






