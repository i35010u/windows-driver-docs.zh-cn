---
title: KSPROPERTY\_分配器\_控制\_遵循\_计数
description: KSPROPERTY\_分配器\_控制\_遵循\_计数属性通知覆盖混音器如何确定要分配的 DirectDraw 表面的数目。 此属性为可选项。
ms.assetid: 3a867554-a6ef-49bd-89e7-e5d09a21609e
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT 流媒体设备
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
ms.openlocfilehash: 04b46f380766a59b4694872a7a02d0166299f206
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832004"
---
# <a name="ksproperty_allocator_control_honor_count"></a>KSPROPERTY\_分配器\_控制\_遵循\_计数


KSPROPERTY\_分配器\_控制\_遵循\_计数属性通知覆盖混音器如何确定要分配的 DirectDraw 表面的数目。 此属性为可选项。

## <span id="ddk_ksproperty_allocator_control_honor_count_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT_KS"></span>


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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 DWORD，用于指定覆盖混音器计算覆盖曲面数量和使用的方式。

<a name="remarks"></a>备注
-------

KSPROPERTY\_分配器\_控制\_遵循\_计数属性请求必须返回1才能强制覆盖混音器使用[**KSPROPERTY\_连接\_** ](ksproperty-connection-allocatorframing.md)中指定的图面数量 ALLOCATORFRAMING知识产权. 返回值为零将导致覆盖混音器计算要分配的表面数。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_连接\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

 

 






