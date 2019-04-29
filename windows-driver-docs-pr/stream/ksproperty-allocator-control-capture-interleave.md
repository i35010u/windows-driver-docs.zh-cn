---
title: KSPROPERTY\_ALLOCATOR\_控制\_捕获\_交错
description: KSPROPERTY\_ALLOCATOR\_控制\_捕获\_交错属性会通知覆盖 Mixer 是否交错捕获有可能。
ms.assetid: ea38289f-2d4e-4613-ba08-c8ab49f6fce7
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE 流式处理媒体设备
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
ms.openlocfilehash: 8191d672fffda3304bf16bce37bf75d7d41133e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390891"
---
# <a name="kspropertyallocatorcontrolcaptureinterleave"></a>KSPROPERTY\_ALLOCATOR\_控制\_捕获\_交错


KSPROPERTY\_ALLOCATOR\_控制\_捕获\_交错属性会通知覆盖 Mixer 是否交错捕获有可能。

## <span id="ddk_ksproperty_allocator_control_capture_interleave_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564274" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564274)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 ulong 值，指定是否可以交错的捕获。

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

[**KSPROPERTY\_ALLOCATOR\_控制\_捕获\_交错\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564274)

 

 






