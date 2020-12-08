---
title: KSPROPERTY \_ BDA \_ 调制 \_ 类型
description: 客户端使用 KSPROPERTY \_ BDA \_ 调制 \_ 类型来控制解调器类型，例如 QPSK 或8VSB。
keywords:
- KSPROPERTY_BDA_MODULATION_TYPE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_MODULATION_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb6ffe5cbb1048a9d08be2970d5b09fe00c30cd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801229"
---
# <a name="ksproperty_bda_modulation_type"></a>KSPROPERTY \_ BDA \_ 调制 \_ 类型


客户端使用 KSPROPERTY \_ BDA \_ 调制 \_ 类型来控制解调器类型，例如 QPSK 或8VSB。

## <span id="ddk_ksproperty_bda_modulation_type_ks"></span><span id="DDK_KSPROPERTY_BDA_MODULATION_TYPE_KS"></span>


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
<td><p>ModulationType</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

ModulationType 枚举类型的返回值标识解调器类型。

KSP **NodeId** \_ 节点的节点标识号指定了解调器节点的标识符。

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


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**ModulationType**](/previous-versions/windows/desktop/mstv/modulationtype)

 

