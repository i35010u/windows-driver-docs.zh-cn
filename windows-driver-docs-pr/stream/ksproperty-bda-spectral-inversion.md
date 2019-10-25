---
title: KSPROPERTY\_BDA\_SPECTRAL\_反转
description: 客户端使用 KSPROPERTY\_BDA\_SPECTRAL\_反转来控制某个解调器节点 SPECTRAL 反转的设置。
ms.assetid: a51dee0b-4a45-4159-978b-27ff6e2333e2
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
ms.openlocfilehash: b39cd4647aee73b9c784e1966388957bf4adcc39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843602"
---
# <a name="ksproperty_bda_spectral_inversion"></a>KSPROPERTY\_BDA\_SPECTRAL\_反转


客户端使用 KSPROPERTY\_BDA\_SPECTRAL\_反转来控制某个解调器节点 SPECTRAL 反转的设置。

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
<td><p>SpectralInversion</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

SpectralInversion 枚举类型的返回值标识 spectral 反转的设置。

KSP\_**节点的节点**标识号指定了解调器节点的标识符。

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


[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**SpectralInversion**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568154(v=vs.85))

 

 






