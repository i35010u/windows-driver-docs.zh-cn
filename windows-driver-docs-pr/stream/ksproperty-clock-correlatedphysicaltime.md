---
title: KSPROPERTY \_ 时钟 \_ CORRELATEDPHYSICALTIME
description: 客户端使用 KSPROPERTY \_ 时钟 \_ CORRELATEDPHYSICALTIME 属性将时钟上的当前物理时间与当前系统时间进行比较。
ms.assetid: 49f74411-1489-4864-9213-e1894128e355
keywords:
- KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME 流媒体设备
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
ms.openlocfilehash: 40f280b4fbd5b62149869afc45c99a9dd7f68249
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190897"
---
# <a name="ksproperty_clock_correlatedphysicaltime"></a>KSPROPERTY \_ 时钟 \_ CORRELATEDPHYSICALTIME


客户端使用 KSPROPERTY \_ 时钟 \_ CORRELATEDPHYSICALTIME 属性将时钟上的当前物理时间与当前系统时间进行比较。

## <span id="ddk_ksproperty_clock_correlatedphysicaltime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_CORRELATEDPHYSICALTIME_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscorrelated_time" data-raw-source="[&lt;strong&gt;KSCORRELATED_TIME&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kscorrelated_time)"><strong>KSCORRELATED_TIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSCORRELATED \_ 时间结构包含 **时间** 成员中的当前时钟时间和 **SystemTime** 成员的相关物理时间。

另请参阅 [KS 时钟](./ks-clocks.md)。

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


[**KSPROPERTY \_ 时钟 \_ PHYSICALTIME**](ksproperty-clock-physicaltime.md)

[**KeQueryPerformanceCounter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kequeryperformancecounter)

 

