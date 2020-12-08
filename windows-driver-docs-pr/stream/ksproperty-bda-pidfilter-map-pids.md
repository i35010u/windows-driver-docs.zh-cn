---
title: KSPROPERTY \_ BDA \_ PIDFILTER \_ 映射 \_ PID
description: 客户端使用 KSPROPERTY \_ BDA \_ PIDFILTER \_ MAP \_ pid 通知 PID 筛选器节点有关应传递到下游筛选器或节点的传输流包的 MPEG2 pid 列表。
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
ms.openlocfilehash: b8a1b0787835a630b9259821f9b98ad83ecf7575
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793345"
---
# <a name="ksproperty_bda_pidfilter_map_pids"></a>KSPROPERTY \_ BDA \_ PIDFILTER \_ 映射 \_ PID


客户端使用 KSPROPERTY \_ BDA \_ PIDFILTER \_ MAP \_ pid 通知 PID 筛选器节点有关应传递到下游筛选器或节点的传输流包的 MPEG2 pid 列表。 此属性还会通知 PID 筛选器节点 (的示例表部分或传输流) 在节点的输出上传递数据时要使用的输出类型。

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
<td><p>BDA_PID_MAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点标识号指定 PID 筛选器节点的标识符。

BDA \_ PID \_ 映射结构描述要从输入流中筛选出的数据的映射。

PID 筛选器节点将随此属性提供的列表与节点当前通过下游传递的 Pid 列表合并。 如果提供的列表中的 PID 已经在 PID 筛选器节点的列表中，则提供的列表的输出类型将优先。 此属性还可用于检索节点输出的数据的类型。 BDA \_ PID \_ 映射结构描述了此输出数据的映射。

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


[**BDA \_ PID \_ 映射**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_pid_map)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

