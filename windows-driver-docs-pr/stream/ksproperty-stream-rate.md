---
title: KSPROPERTY\_STREAM\_RATE
description: KSPROPERTY\_流\_速率属性的工作原理与 KSPROPERTY 结合\_流\_RATECAPABILITY 以及用于查询的功能的 pin 后设置段的速率。
ms.assetid: 125dcd39-fb67-4d9f-81af-b7f4c0e566cc
keywords:
- KSPROPERTY_STREAM_RATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_RATE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 364579feb88b0e98ce28825cba30b74a775145be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379955"
---
# <a name="kspropertystreamrate"></a>KSPROPERTY\_STREAM\_RATE


KSPROPERTY\_流\_速率属性的工作原理与结合[ **KSPROPERTY\_流\_RATECAPABILITY** ](ksproperty-stream-ratecapability.md)以及用于设置速率查询的功能的 pin 后的段。

## <span id="ddk_ksproperty_stream_rate_ks"></span><span id="DDK_KSPROPERTY_STREAM_RATE_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566752" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566752)"><strong>KSRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_流\_应实现率，如果 pin 允许速率更改或拓扑结构上相关的插针之间的接口不同，会导致正在使用不同的时间戳格式。

可以修改的数据来重新采样速率的 pin 支持该属性或时间戳更改，以便可以更接近于 1.0 的名义利率请求的速率。

读取该属性返回的当前速率和段。 设置新段的速率将替换任何当前速率的设置。 以这种方式，停止快进请求可以通过请求速率设置为 1.0，它始终应接受。 如果指定的速率不可以，pin 可以拒绝该请求而不是尝试最佳的设置。

率设置和查询都使用[ **KSRATE** ](https://msdn.microsoft.com/library/windows/hardware/ff566752)结构，它指定演示文稿开始时间、 持续时间和速率。 速率更改只能在中执行暂停或运行状态，并将更改为任何其他状态后停止。 按百分比或 pin 是调整和相同的格式返回的当前设置的名义 1.0 速率过指定的速率变化。

此属性也应该用于将接口和时间单位在以前的属性中指定，应实现上更改 pin，之间的接口的筛选器中，即使不支持的更改速率。 例如，筛选器支持 KSINTERFACE\_标准\_在一个位置固定，并将转换到 KSINTERFACE\_标准\_流式处理的另一个插针相关的拓扑可能不支持的更改速率。 筛选器应能够接受 pin 和任一接口上的更改请求，并将更改为其自己的接口和单位，尽管速率将保持不变。

如果 pin 还会生成一个时钟，因为使用时钟速率匹配任何客户端应为斜率为像 1.0 名义上的费率运行基础硬件的速率变化不得更改物理时间的斜率。 这意味着不能确保物理时钟斜率保持一致而无需大量偏差的 pin 不能接受速率调整请求。

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


[**KSPROPERTY\_STREAM\_RATECAPABILITY**](ksproperty-stream-ratecapability.md)

[**KSRATE**](https://msdn.microsoft.com/library/windows/hardware/ff566752)

 

 






