---
title: KSPROPERTY\_BDA\_INNER\_FEC\_RATE
description: 客户端使用 KSPROPERTY\_BDA\_内部\_FEC\_速率以控制的二进制卷积方案用于内部的前向纠错 (FEC) 解调器节点类型。
ms.assetid: d5bf0ce0-d383-431f-85de-3d00f4831619
keywords:
- KSPROPERTY_BDA_INNER_FEC_RATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_INNER_FEC_RATE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0a9e2d28160fbafc8d722851f77043ca10834ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359681"
---
# <a name="kspropertybdainnerfecrate"></a>KSPROPERTY\_BDA\_INNER\_FEC\_RATE


客户端使用 KSPROPERTY\_BDA\_内部\_FEC\_速率以控制的二进制卷积方案用于内部的前向纠错 (FEC) 解调器节点类型。

## <span id="ddk_ksproperty_bda_inner_fec_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_INNER_FEC_RATE_KS"></span>


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
<td><p>BinaryConvolutionCodeRate</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BinaryConvolutionCodeRate 枚举类型中的返回的值标识二进制卷积方案。

**NodeId** KSP 成员\_节点指定解调器节点的标识符。

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


[**BinaryConvolutionCodeRate**](https://msdn.microsoft.com/library/windows/hardware/ff556566)

[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






