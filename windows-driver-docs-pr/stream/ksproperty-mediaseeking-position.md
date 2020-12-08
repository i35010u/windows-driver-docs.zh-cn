---
title: KSPROPERTY \_ MEDIASEEKING \_ 位置
description: KSPROPERTY \_ MEDIASEEKING \_ POSITION 检索筛选器的媒体时间。
keywords:
- KSPROPERTY_MEDIASEEKING_POSITION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_POSITION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46bd9a7b0de3186baf2fa92cdad412abbac812f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821783"
---
# <a name="ksproperty_mediaseeking_position"></a>KSPROPERTY \_ MEDIASEEKING \_ 位置


KSPROPERTY \_ MEDIASEEKING \_ POSITION 检索筛选器的媒体时间。

## <span id="ddk_ksproperty_mediaseeking_position_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_POSITION_KS"></span>


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
<td><p>否</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

媒体时间作为 LONGLONG 类型的值返回。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[KSPROPSETID \_ MediaSeeking](kspropsetid-mediaseeking.md)

