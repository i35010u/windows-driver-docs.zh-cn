---
title: KSPROPERTY \_ BDA \_ 表 \_ 部分
description: '\_ \_ \_ 当在节点的输出上传递数据时，客户端使用 KSPROPERTY BDA 表部分来通知节点要使用的表部分。'
keywords:
- KSPROPERTY_BDA_TABLE_SECTION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TABLE_SECTION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e52b7e92484a151e16a32bebcfa645476f8b134
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799293"
---
# <a name="ksproperty_bda_table_section"></a>KSPROPERTY \_ BDA \_ 表 \_ 部分


\_ \_ \_ 当在节点的输出上传递数据时，客户端使用 KSPROPERTY BDA 表部分来通知节点要使用的表部分。

## <span id="ddk_ksproperty_bda_table_section_ks"></span><span id="DDK_KSPROPERTY_BDA_TABLE_SECTION_KS"></span>


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
<td><p>BDA_TABLE_SECTION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** 节点的节点成员 \_ 指定了 LNB 放大器节点。

"BDA \_ 表" \_ 部分结构描述了表部分。

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


[**BDA \_ 表 \_ 部分**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_table_section)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

