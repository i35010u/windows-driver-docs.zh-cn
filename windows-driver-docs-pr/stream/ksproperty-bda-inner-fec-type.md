---
title: KSPROPERTY\_BDA\_INNER\_FEC\_TYPE
description: 客户端使用 KSPROPERTY\_BDA\_内部\_FEC\_类型来控制解调器节点的内部转发错误纠错 (FEC) 类型。
ms.assetid: e6640d89-cf75-4073-98fb-2a877d6c38d3
keywords:
- KSPROPERTY_BDA_INNER_FEC_TYPE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_INNER_FEC_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bd3917e01a4d1a9f4cadc50959f0cd07866fad9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364853"
---
# <a name="kspropertybdainnerfectype"></a>KSPROPERTY\_BDA\_INNER\_FEC\_TYPE


客户端使用 KSPROPERTY\_BDA\_内部\_FEC\_类型来控制解调器节点的内部转发错误纠错 (FEC) 类型。

## <span id="ddk_ksproperty_bda_inner_fec_type_ks"></span><span id="DDK_KSPROPERTY_BDA_INNER_FEC_TYPE_KS"></span>


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
<td><p>FECMethod</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

FECMethod 枚举类型中的返回的值标识 FEC 类型。

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


[**FECMethod**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/fecmethod)

[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






