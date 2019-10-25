---
title: KSPROPERTY\_分配器\_控制\_捕获\_交错
description: 如果可能，KSPROPERTY\_分配器\_控制\_捕获\_交错属性通知重叠混音器。
ms.assetid: ea38289f-2d4e-4613-ba08-c8ab49f6fce7
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
ms.openlocfilehash: f90750744062dc0de3b7f112f44fa773701977a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832008"
---
# <a name="ksproperty_allocator_control_capture_interleave"></a>KSPROPERTY\_分配器\_控制\_捕获\_交错


如果可能，KSPROPERTY\_分配器\_控制\_捕获\_交错属性通知重叠混音器。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，指定是否可以交错捕获。

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

[**KSPROPERTY\_分配器\_控制\_捕获\_交错\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_interleave_s)

 

 






