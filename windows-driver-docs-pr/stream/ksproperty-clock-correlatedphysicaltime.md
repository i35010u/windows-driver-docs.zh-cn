---
title: KSPROPERTY\_时钟\_CORRELATEDPHYSICALTIME
description: 客户端使用 KSPROPERTY\_时钟\_CORRELATEDPHYSICALTIME 属性进行比较的当前系统时间时钟的当前物理时间。
ms.assetid: 49f74411-1489-4864-9213-e1894128e355
keywords:
- KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f8bc8814afb2ae27dbb68405a842ead23dd0560
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342863"
---
# <a name="kspropertyclockcorrelatedphysicaltime"></a>KSPROPERTY\_时钟\_CORRELATEDPHYSICALTIME


客户端使用 KSPROPERTY\_时钟\_CORRELATEDPHYSICALTIME 属性进行比较的当前系统时间时钟的当前物理时间。

## <span id="ddk_ksproperty_clock_correlatedphysicaltime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561033" data-raw-source="[&lt;strong&gt;KSCORRELATED_TIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561033)"><strong>KSCORRELATED_TIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSCORRELATED\_时间结构包含在当前的时钟时间**时间**成员和相关物理时间**SystemTime**成员。

另请参阅[KS 时钟](https://msdn.microsoft.com/library/windows/hardware/ff567307)。

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


[**KSPROPERTY\_CLOCK\_PHYSICALTIME**](ksproperty-clock-physicaltime.md)

[**KeQueryPerformanceCounter**](https://msdn.microsoft.com/library/windows/hardware/ff553053)

 

 






