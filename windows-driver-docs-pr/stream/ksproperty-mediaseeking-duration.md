---
title: KSPROPERTY\_MEDIASEEKING\_持续时间
description: KSPROPERTY\_MEDIASEEKING\_持续时间属性检索对筛选器的媒体持续时间。
ms.assetid: f84ff468-7cf6-4948-afee-a28ee365760d
keywords:
- KSPROPERTY_MEDIASEEKING_DURATION 流式处理媒体设备
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
ms.openlocfilehash: 71d94274d320a34c1297a511f29e36410c4343af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576797"
---
# <a name="kspropertymediaseekingduration"></a>KSPROPERTY\_MEDIASEEKING\_持续时间


KSPROPERTY\_MEDIASEEKING\_持续时间属性检索对筛选器的媒体持续时间。

## <span id="ddk_ksproperty_mediaseeking_duration_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_DURATION_KS"></span>


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
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回类型 LONGLONG 的值为媒体持续时间。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






