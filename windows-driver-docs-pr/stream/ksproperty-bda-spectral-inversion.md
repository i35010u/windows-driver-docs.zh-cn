---
title: KSPROPERTY \_ BDA \_ SPECTRAL \_ 反转
description: 客户端使用 KSPROPERTY \_ BDA \_ SPECTRAL \_ 反转来控制某个解调器节点 SPECTRAL 反转的设置。
keywords:
- KSPROPERTY_BDA_SPECTRAL_INVERSION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SPECTRAL_INVERSION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea913bf9eec2e01af65db26be66ed737f65b8310
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823701"
---
# <a name="ksproperty_bda_spectral_inversion"></a>KSPROPERTY \_ BDA \_ SPECTRAL \_ 反转


客户端使用 KSPROPERTY \_ BDA \_ SPECTRAL \_ 反转来控制某个解调器节点 SPECTRAL 反转的设置。

## <span id="ddk_ksproperty_bda_spectral_inversion_ks"></span><span id="DDK_KSPROPERTY_BDA_SPECTRAL_INVERSION_KS"></span>


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
<td><p>SpectralInversion</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

SpectralInversion 枚举类型的返回值标识 spectral 反转的设置。

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

[**SpectralInversion**](/previous-versions/windows/hardware/drivers/ff568154(v=vs.85))

 

