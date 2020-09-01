---
title: KSPROPERTY \_ 时钟 \_ 时间
description: 客户端使用 KSPROPERTY \_ 时钟 \_ 时间属性来确定时钟上当前的呈现时间。
ms.assetid: 42bae8fa-bff0-4411-bf32-5aa4da3e4f02
keywords:
- KSPROPERTY_CLOCK_TIME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_TIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d56866625a27e2b89bdb1d92d3ce6b09cf02073
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192367"
---
# <a name="ksproperty_clock_time"></a>KSPROPERTY \_ 时钟 \_ 时间


客户端使用 KSPROPERTY \_ 时钟 \_ 时间属性来确定时钟上当前的呈现时间。

## <span id="ddk_ksproperty_clock_time_ks"></span><span id="DDK_KSPROPERTY_CLOCK_TIME_KS"></span>


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
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

此属性返回类型为 LONGLONG 的值，指定当前演示时间（以100毫微秒为单位）。

与物理时间不同，时钟的显示时间可能会反转。 时钟的显示时间通常表示基础数据流上的时间戳。 例如，DVD 播放机的时钟可将 DVD 中当前位置的时间戳报告为其表示时间。

不需要使用时钟来支持100毫微秒的分辨率。 若要确定时钟分辨率，客户端可以使用 [**KSPROPERTY \_ 时钟 \_ 解析**](ksproperty-clock-resolution.md) 请求。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[KSPROPSETID \_ 时钟](kspropsetid-clock.md)

 

