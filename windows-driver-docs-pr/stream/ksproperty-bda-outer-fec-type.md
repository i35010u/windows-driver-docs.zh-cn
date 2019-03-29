---
title: KSPROPERTY\_BDA\_OUTER\_FEC\_TYPE
description: 客户端使用 KSPROPERTY\_BDA\_OUTER\_FEC\_类型来控制解调器节点的外部转发错误纠错 (FEC) 类型。
ms.assetid: 952fd2d6-20c8-4fb3-a92a-1e6bcedfd68b
keywords:
- KSPROPERTY_BDA_OUTER_FEC_TYPE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_OUTER_FEC_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e42e7d23beebd1cc5949a10473d5bdc8dcd081e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565737"
---
# <a name="kspropertybdaouterfectype"></a>KSPROPERTY\_BDA\_OUTER\_FEC\_TYPE


客户端使用 KSPROPERTY\_BDA\_OUTER\_FEC\_类型来控制解调器节点的外部转发错误纠错 (FEC) 类型。

## <span id="ddk_ksproperty_bda_outer_fec_type_ks"></span><span id="DDK_KSPROPERTY_BDA_OUTER_FEC_TYPE_KS"></span>


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


[**FECMethod**](https://msdn.microsoft.com/library/windows/hardware/ff559594)

[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






