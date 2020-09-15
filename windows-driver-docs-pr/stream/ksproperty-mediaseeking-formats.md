---
title: KSPROPERTY \_ MEDIASEEKING \_ 格式
description: KSPROPERTY \_ MEDIASEEKING \_ FORMATS 属性检索筛选器支持的媒体时间格式。 此信息作为多项属性返回。
ms.assetid: 6d01737e-baef-4a65-90c7-3838cb19b4c9
keywords:
- KSPROPERTY_MEDIASEEKING_FORMATS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_FORMATS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccec5977dadef58d97287cd8606e72735820787
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102694"
---
# <a name="ksproperty_mediaseeking_formats"></a>KSPROPERTY \_ MEDIASEEKING \_ 格式


KSPROPERTY \_ MEDIASEEKING \_ FORMATS 属性检索筛选器支持的媒体时间格式。 此信息作为多项属性返回。

## <span id="ddk_ksproperty_mediaseeking_formats_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_FORMATS_KS"></span>


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
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性可以返回多个项属性。 请求者负责提供足够大小的缓冲区。

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

## <a name="see-also"></a>另请参阅


[KSPROPSETID \_ MediaSeeking](kspropsetid-mediaseeking.md)

