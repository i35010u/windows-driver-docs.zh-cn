---
title: KSPROPERTY \_ 流 \_ 速率
description: KSPROPERTY \_ 流 \_ 速率属性与 KSPROPERTY \_ stream RATECAPABILITY 结合 \_ 使用，用于设置查询 pin 功能后的段速率。
ms.assetid: 125dcd39-fb67-4d9f-81af-b7f4c0e566cc
keywords:
- KSPROPERTY_STREAM_RATE 流媒体设备
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
ms.openlocfilehash: 9b3b05038ca86b8a5bed30d0343ae891fe1fad86
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186535"
---
# <a name="ksproperty_stream_rate"></a>KSPROPERTY \_ 流 \_ 速率


KSPROPERTY \_ 流 \_ 速率属性与 [**KSPROPERTY \_ stream \_ RATECAPABILITY**](ksproperty-stream-ratecapability.md) 结合使用，用于设置查询 pin 功能后的段速率。

## <span id="ddk_ksproperty_stream_rate_ks"></span><span id="DDK_KSPROPERTY_STREAM_RATE_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)"><strong>KSRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

\_ \_ 如果 pin 允许速率改变，或界定闭合相关 pin 之间的接口不同，并使用不同的时间戳格式，则应该实现 KSPROPERTY 流速率。

此属性由 pin 支持，可以通过重新采样或时间戳更改来修改数据的速率，以使请求的速率更接近标称速率1.0。

读取属性将返回当前速率和段。 设置新段的速率将替换任何当前速率设置。 通过这种方式，可以通过请求1.0 的费率设置来停止快进请求，该设置应始终接受。 如果无法获得指定的速率，则 pin 可以拒绝请求，而不是尝试最佳设置。

Rate 设置和查询都使用 [**KSRATE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate) 结构来指定演示开始、持续时间和速度。 只能在 "暂停" 或 "运行" 状态中执行速率更改，并在更改为任何其他状态后停止。 速率更改是根据 pin 要调整的1.0 标称百分比或下的百分比指定的，当前设置以相同的格式返回。

此属性还应用于转换在上一个属性中指定的接口和时间单位，并且应在更改 pin 之间的接口的筛选器上实现，即使不支持速率更改也是如此。 例如，在 \_ 一个插针上支持 KSINTERFACE 标准位置的筛选器， \_ 并且 \_ \_ 在拓扑相关的另一个 PIN 上转换为 KSINTERFACE standard 流式处理可能不支持速率更改。 筛选器应该能够在任一 pin 上执行更改请求，并可以对其自己的接口和单位进行更改，但是速度会保持不变。

如果 pin 还生成时钟，则速率更改不能更改物理时间的斜率，因为使用时钟进行速率匹配的任何客户端都需要使用时钟进行速率匹配的客户端，就像以名义1.0 费率运行基础硬件一样。 这意味着，无法确保物理时钟斜度保持一致，且不会产生严重偏差的 pin 无法接受速率调整请求。

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


[**KSPROPERTY \_ 流 \_ RATECAPABILITY**](ksproperty-stream-ratecapability.md)

[**KSRATE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)

 

