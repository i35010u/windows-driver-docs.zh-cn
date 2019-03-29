---
title: KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PIDS
description: 客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID 通知 PID 筛选有关标识特定的 Pid 来筛选从输入流的数据包的节点 （即，停止从输入到输出将传递）。
ms.assetid: 111d8857-84f4-4a7f-8771-ea6537c4c592
keywords:
- KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS 流式处理媒体设备
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
ms.openlocfilehash: 6a2da0d3a24e845256fbe9bf220a7c1dff2c3137
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566224"
---
# <a name="kspropertybdapidfilterunmappids"></a>KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PIDS


客户端使用 KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID 通知 PID 筛选有关标识特定的 Pid 来筛选从输入流的数据包的节点 （即，停止从输入到输出将传递）。

## <span id="ddk_ksproperty_bda_pidfilter_unmap_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS_KS"></span>


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
<td><p>BDA_PID_UNMAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定 PID 筛选器节点的标识符。

BDA\_PID\_UNMAP 结构描述的带有特定的 Pid 来筛选从输入流的数据包的映射。

不按节点传递此列表中的任何 PID 将被忽略。

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


[**BDA\_PID\_UNMAP**](https://msdn.microsoft.com/library/windows/hardware/ff556540)

[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






