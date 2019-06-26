---
title: KSPROPERTY\_BDA\_PIDFILTER\_LIST\_PIDS
description: 客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_列表\_PID 从 PID 筛选器节点中检索标识的节点从输入流传递到输出流的数据包的组及其 Pid 的列表。
ms.assetid: fc7dc0af-af74-4bd1-b99c-f06de25aae3c
keywords:
- KSPROPERTY_BDA_PIDFILTER_LIST_PIDS 流式处理媒体设备
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
ms.openlocfilehash: 8ed4cd8aa746244ba0f00386564c1bbdacac9e79
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368146"
---
# <a name="kspropertybdapidfilterlistpids"></a>KSPROPERTY\_BDA\_PIDFILTER\_LIST\_PIDS


客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_列表\_PID 从 PID 筛选器节点中检索标识的节点从输入流传递到输出流的数据包的组及其 Pid 的列表。

## <span id="ddk_ksproperty_bda_pidfilter_list_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_LIST_PIDS_KS"></span>


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
<td><p>Pid 的列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定 PID 筛选器节点的标识符。

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


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






