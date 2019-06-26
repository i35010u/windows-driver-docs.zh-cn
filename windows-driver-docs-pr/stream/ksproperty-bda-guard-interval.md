---
title: KSPROPERTY\_BDA\_防护\_间隔
description: 客户端使用 KSPROPERTY\_BDA\_防止\_间隔来控制解调器节点的防护间隔的设置。
ms.assetid: 7c0c6c5e-94fd-4013-9778-d41568ae9f0b
keywords:
- KSPROPERTY_BDA_GUARD_INTERVAL 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_GUARD_INTERVAL
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7667081ba0e2191f9aaef93af4b91d9ef4618c61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364863"
---
# <a name="kspropertybdaguardinterval"></a>KSPROPERTY\_BDA\_防护\_间隔


客户端使用 KSPROPERTY\_BDA\_防止\_间隔来控制解调器节点的防护间隔的设置。

## <span id="ddk_ksproperty_bda_guard_interval_ks"></span><span id="DDK_KSPROPERTY_BDA_GUARD_INTERVAL_KS"></span>


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
<td><p>GuardInterval</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

GuardInterval 枚举类型中的返回的值标识防护间隔设置。

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


[**GuardInterval**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/guardinterval)

[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






