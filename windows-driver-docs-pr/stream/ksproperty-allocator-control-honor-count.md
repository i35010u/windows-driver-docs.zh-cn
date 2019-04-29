---
title: KSPROPERTY\_ALLOCATOR\_控制\_遵循\_计数
description: KSPROPERTY\_ALLOCATOR\_控制\_遵循\_计数属性通知覆盖 Mixer 如何确定 DirectDraw surface 分配数。 此属性为可选项。
ms.assetid: 3a867554-a6ef-49bd-89e7-e5d09a21609e
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4e27864106eee0627ccae1b1da5ee76eb4d814f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354517"
---
# <a name="kspropertyallocatorcontrolhonorcount"></a>KSPROPERTY\_ALLOCATOR\_控制\_遵循\_计数


KSPROPERTY\_ALLOCATOR\_控制\_遵循\_计数属性通知覆盖 Mixer 如何确定 DirectDraw surface 分配数。 此属性为可选项。

## <span id="ddk_ksproperty_allocator_control_honor_count_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 dword 值，指定如何覆盖 Mixer 计算数和使用的覆盖面。

<a name="remarks"></a>备注
-------

KSPROPERTY\_ALLOCATOR\_控制\_荣誉\_计数属性请求必须返回 1，以强制覆盖 Mixer 使用数量的图面中指定[ **KSPROPERTY\_连接\_ALLOCATORFRAMING** ](ksproperty-connection-allocatorframing.md)属性。 返回值为 0 会导致覆盖 Mixer 来计算分配多少表面。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_连接\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

 

 






