---
title: KSPROPERTY \_ 分配器 \_ 控件 \_ 捕获 \_ 交错
description: '\_ \_ \_ \_ 如果可能交错捕获，KSPROPERTY 分配器控制捕获交错属性会通知覆盖混音器。'
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b77c8808e8ea2ef1f59a4f5b8894b2a3f5274f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840571"
---
# <a name="ksproperty_allocator_control_capture_interleave"></a>KSPROPERTY \_ 分配器 \_ 控件 \_ 捕获 \_ 交错


\_ \_ \_ \_ 如果可能交错捕获，KSPROPERTY 分配器控制捕获交错属性会通知覆盖混音器。

## <span id="ddk_ksproperty_allocator_control_capture_interleave_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是 ULONG，它指定是否可以交错捕获。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ 分配器 \_ 控件 \_ 捕获 \_ 交错 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s)

