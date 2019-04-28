---
title: KSPROPERTY\_时钟\_时间
description: 客户端使用 KSPROPERTY\_时钟\_时间属性来确定上一个时钟的当前呈现时间。
ms.assetid: 42bae8fa-bff0-4411-bf32-5aa4da3e4f02
keywords:
- KSPROPERTY_CLOCK_TIME 流式处理媒体设备
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
ms.openlocfilehash: dd165c7c7364cb0c822790f637e0df67927495d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330287"
---
# <a name="kspropertyclocktime"></a>KSPROPERTY\_时钟\_时间


客户端使用 KSPROPERTY\_时钟\_时间属性来确定上一个时钟的当前呈现时间。

## <span id="ddk_ksproperty_clock_time_ks"></span><span id="DDK_KSPROPERTY_CLOCK_TIME_KS"></span>


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

此属性返回类型 LONGLONG，以 100 毫微秒为单位指定当前的呈现时间的值。

可以撤消的一个时钟的呈现时间，与物理时间不同。 时钟的呈现时间通常表示基础数据流上的时间戳。 例如，DVD 播放机的时钟可以报告中的当前位置 DVD 作为其呈现时间的时间戳。

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


[KSPROPSETID\_时钟](kspropsetid-clock.md)

 

 






