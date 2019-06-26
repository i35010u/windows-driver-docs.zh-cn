---
title: KSPROPERTY\_BDA\_PIDFILTER\_MAP\_PIDS
description: 客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_映射\_PID 通知 PID 筛选节点有关 MPEG2 Pid 的传输流数据包的应传递到下游的筛选器或节点的列表。
ms.assetid: 33d2775c-308a-4af0-81ae-b174990926ad
keywords:
- KSPROPERTY_BDA_PIDFILTER_MAP_PIDS 流式处理媒体设备
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
ms.openlocfilehash: f6ef7a40a5ea937cd5bfb8344df62acedb4d69e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368853"
---
# <a name="kspropertybdapidfiltermappids"></a>KSPROPERTY\_BDA\_PIDFILTER\_MAP\_PIDS


客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_映射\_PID 通知 PID 筛选节点有关 MPEG2 Pid 的传输流数据包的应传递到下游的筛选器或节点的列表。 此属性还通知 PID 筛选器节点的节点上提供的数据时要使用何种输出类型 （例如表节或传输流） 的输出。

## <span id="ddk_ksproperty_bda_pidfilter_map_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_MAP_PIDS_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BDA_PID_MAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定 PID 筛选器节点的标识符。

BDA\_PID\_站点地图结构描述要筛选出的输入流的数据的映射。

PID 筛选器节点将与此属性与 Pid 列表节点当前传递下游所提供的列表。 如果提供的列表中 PID 已 PID 筛选器节点的列表中，提供的列表的输出类型将优先。 此属性还用于检索的输出节点的数据类型。 BDA\_PID\_站点地图结构介绍了此输出数据的映射。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BDA\_PID\_MAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdatypes/ns-bdatypes-_bda_pid_map)

[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






