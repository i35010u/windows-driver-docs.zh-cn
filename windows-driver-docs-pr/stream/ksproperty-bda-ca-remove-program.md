---
title: KSPROPERTY\_BDA\_CA\_删除\_程序
description: 客户端使用 KSPROPERTY\_BDA\_CA\_删除\_程序以防止访问特定程序。
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
ms.openlocfilehash: 3ae0ea5d5039c6ecce027e553154aa068418e7e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842151"
---
# <a name="ksproperty_bda_ca_remove_program"></a>KSPROPERTY\_BDA\_CA\_删除\_程序


客户端使用 KSPROPERTY\_BDA\_CA\_删除\_程序以防止访问特定程序。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSEVENT\_BDA\_PROGRAM\_FLOW\_状态\_更改**](ksevent-bda-program-flow-status-changed.md)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






