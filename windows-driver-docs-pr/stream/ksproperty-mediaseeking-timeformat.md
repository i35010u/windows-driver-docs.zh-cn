---
title: KSPROPERTY\_MEDIASEEKING\_TIMEFORMAT
description: KSPROPERTY\_MEDIASEEKING\_TIMEFORMAT 属性检索筛选器的当前媒体时间格式。
ms.assetid: 3a7b6873-7351-4e87-8fa7-a804894c56bb
keywords:
- KSPROPERTY_MEDIASEEKING_TIMEFORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_TIMEFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5c8ca889727585293e9d4d2b02923dc74c928e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346488"
---
# <a name="kspropertymediaseekingtimeformat"></a>KSPROPERTY\_MEDIASEEKING\_TIMEFORMAT


KSPROPERTY\_MEDIASEEKING\_TIMEFORMAT 属性检索筛选器的当前媒体时间格式。

## <span id="ddk_ksproperty_mediaseeking_timeformat_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_TIMEFORMAT_KS"></span>


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
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

属性将返回的当前媒体时间格式设置为时间格式的 GUID。

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

 

 






