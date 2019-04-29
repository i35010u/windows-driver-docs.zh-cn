---
title: KSPROPERTY\_时钟\_PHYSICALTIME
description: 客户端使用 KSPROPERTY\_时钟\_物理\_时间属性来确定当前物理时钟的时间。
ms.assetid: cc747fd4-1df0-4d44-b43e-b43532c1228b
keywords:
- KSPROPERTY_CLOCK_PHYSICALTIME 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_PHYSICALTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6acdc9700f040d9cd2ee4e9f901fff31b81e0ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357057"
---
# <a name="kspropertyclockphysicaltime"></a>KSPROPERTY\_时钟\_PHYSICALTIME


客户端使用 KSPROPERTY\_时钟\_物理\_时间属性来确定当前物理时钟的时间。

## <span id="ddk_ksproperty_clock_physicaltime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_PHYSICALTIME_KS"></span>


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
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回类型 LONGLONG，表示当前物理时间以 100 毫微秒为单位的值。

物理时钟的时间是不断进行的计数器。 与不同的呈现时间，它无法撤消。

时钟不需要支持 100 纳秒解决方法。 若要确定时钟分辨率，客户端可以使用[ **KSPROPERTY\_时钟\_解析**](ksproperty-clock-resolution.md)请求。

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


[**KSPROPERTY\_时钟\_CORRELATEDPHYSICALTIME**](ksproperty-clock-correlatedphysicaltime.md)

[**KSPROPERTY\_时钟\_CORRELATEDTIME**](ksproperty-clock-correlatedtime.md)

 

 






