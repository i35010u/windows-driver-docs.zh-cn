---
title: KSPROPERTY\_BDA\_INNER\_FEC\_速率
description: 客户端使用 KSPROPERTY\_BDA\_INNER\_FEC\_速率来控制用于某个解调器节点的内部正向纠错（FEC）类型的二进制卷积方案。
ms.assetid: d5bf0ce0-d383-431f-85de-3d00f4831619
keywords:
- KSPROPERTY_BDA_INNER_FEC_RATE 流媒体设备
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
ms.openlocfilehash: 98b84bfac03807315a6494cac496cc613cbca7e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842141"
---
# <a name="ksproperty_bda_inner_fec_rate"></a>KSPROPERTY\_BDA\_INNER\_FEC\_速率


客户端使用 KSPROPERTY\_BDA\_INNER\_FEC\_速率来控制用于某个解调器节点的内部正向纠错（FEC）类型的二进制卷积方案。

## <span id="ddk_ksproperty_bda_inner_fec_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_INNER_FEC_RATE_KS"></span>


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
<td><p>BinaryConvolutionCodeRate</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BinaryConvolutionCodeRate 枚举类型返回的值标识二进制卷积方案。

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


[**BinaryConvolutionCodeRate**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/binaryconvolutioncoderate)

[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






