---
title: KSPROPERTY \_ MEDIASEEKING \_ DURATION
description: KSPROPERTY \_ MEDIASEEKING \_ duration 属性检索筛选器上的媒体持续时间。
ms.assetid: f84ff468-7cf6-4948-afee-a28ee365760d
keywords:
- KSPROPERTY_MEDIASEEKING_DURATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_DURATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69503d208badc800919c793e73b6a3b7eb145f9b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107166"
---
# <a name="ksproperty_mediaseeking_duration"></a>KSPROPERTY \_ MEDIASEEKING \_ DURATION


KSPROPERTY \_ MEDIASEEKING \_ duration 属性检索筛选器上的媒体持续时间。

## <span id="ddk_ksproperty_mediaseeking_duration_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_DURATION_KS"></span>


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

此属性将媒体持续时间返回为 LONGLONG 类型的值。

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

