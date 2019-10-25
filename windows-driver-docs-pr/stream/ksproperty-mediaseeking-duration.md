---
title: KSPROPERTY\_MEDIASEEKING\_持续时间
description: KSPROPERTY\_MEDIASEEKING\_DURATION 属性检索筛选器上的媒体持续时间。
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
ms.openlocfilehash: 394b6012de4a26530ac32086439a6d8ac5f64c95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842300"
---
# <a name="ksproperty_mediaseeking_duration"></a>KSPROPERTY\_MEDIASEEKING\_持续时间


KSPROPERTY\_MEDIASEEKING\_DURATION 属性检索筛选器上的媒体持续时间。

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
<td><p>无</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






