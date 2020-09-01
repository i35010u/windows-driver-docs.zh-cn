---
title: KSPROPERTY \_ BDA \_ CA \_ 删除 \_ 程序
description: 客户端使用 KSPROPERTY \_ BDA \_ CA \_ REMOVE \_ PROGRAM 来阻止对特定程序的访问。
ms.assetid: 07792113-6d47-4836-8db2-6960fb14ab87
keywords:
- KSPROPERTY_BDA_CA_REMOVE_PROGRAM 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_REMOVE_PROGRAM
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ef02a03bc7929d07a2348c0f9c1c382a28b501a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188169"
---
# <a name="ksproperty_bda_ca_remove_program"></a>KSPROPERTY \_ BDA \_ CA \_ 删除 \_ 程序


客户端使用 KSPROPERTY \_ BDA \_ CA \_ REMOVE \_ PROGRAM 来阻止对特定程序的访问。

## <span id="ddk_ksproperty_bda_ca_remove_program_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_REMOVE_PROGRAM_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

属性值指定要使其无法访问的程序。

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


[**KSEVENT \_ BDA \_ 程序 \_ 流 \_ 状态 \_ 已更改**](ksevent-bda-program-flow-status-changed.md)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

