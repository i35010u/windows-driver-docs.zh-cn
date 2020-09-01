---
title: KSPROPERTY \_ 时钟 \_ 解析
description: 客户端使用 KSPROPERTY \_ 时钟 \_ 解析属性来确定时钟的精度。
ms.assetid: 3e92a4fb-207f-449a-bc70-aa8028b4f8f1
keywords:
- KSPROPERTY_CLOCK_RESOLUTION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_RESOLUTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7caeaa7ffe3cf569131f3b126dbeb58d4ca0229
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191083"
---
# <a name="ksproperty_clock_resolution"></a>KSPROPERTY \_ 时钟 \_ 解析


客户端使用 KSPROPERTY \_ 时钟 \_ 解析属性来确定时钟的精度。

## <span id="ddk_ksproperty_clock_resolution_ks"></span><span id="DDK_KSPROPERTY_CLOCK_RESOLUTION_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksresolution" data-raw-source="[&lt;strong&gt;KSRESOLUTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksresolution)"><strong>KSRESOLUTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**错误**成员中引入的延迟以及**粒度**成员中的延迟。 例如， **精度** 为1到2的 **错误** 的时钟将能够每300毫微秒发出时钟事件通知。

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


[**KSCLOCK \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksclock_dispatch)

[**KSRESOLUTION**](/windows-hardware/drivers/ddi/ks/ns-ks-ksresolution)

[**KSPROPERTY \_ 时钟 \_ PHYSICALTIME**](ksproperty-clock-physicaltime.md)

 

