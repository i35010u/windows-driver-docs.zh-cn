---
title: KSPROPERTY\_BDA\_CA\_SET\_PROGRAM\_PIDS
description: 客户端使用 KSPROPERTY\_BDA\_CA\_设置\_程序\_PID 在特定的程序中设置的数据包标识符列表。
ms.assetid: 5cc049f7-df97-4739-8ec4-22ab646781a6
keywords:
- KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS 流式处理媒体设备
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
ms.openlocfilehash: 69a83c6d750605c9ab00d4f4b3c989f26449663e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325223"
---
# <a name="kspropertybdacasetprogrampids"></a>KSPROPERTY\_BDA\_CA\_SET\_PROGRAM\_PIDS


客户端使用 KSPROPERTY\_BDA\_CA\_设置\_程序\_PID 在特定的程序中设置的数据包标识符列表。

## <span id="ddk_ksproperty_bda_ca_set_program_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS_KS"></span>


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
<td><p>BDA_PROGRAM_PID_LIST</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BDA\_程序\_PID\_列表结构包含的指定程序的数据包标识符列表。

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


[**BDA\_PROGRAM\_PID\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff556549)

[**KSEVENT\_BDA\_程序\_流\_状态\_已更改**](ksevent-bda-program-flow-status-changed.md)

[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






