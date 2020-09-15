---
title: KSPROPERTY \_ 流 \_ PRESENTATIONTIME
description: KSPROPERTY \_ STREAM \_ PRESENTATIONTIME 属性用于检索和设置筛选器 pin 的当前演示时间。
ms.assetid: fb7bcd04-e600-4bab-b7e7-2b99e2bc0a6c
keywords:
- KSPROPERTY_STREAM_PRESENTATIONTIME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_PRESENTATIONTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4957ea140a5a292aa0c5993ac7df6bdcb8977d3a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105716"
---
# <a name="ksproperty_stream_presentationtime"></a>KSPROPERTY \_ 流 \_ PRESENTATIONTIME


KSPROPERTY \_ STREAM \_ PRESENTATIONTIME 属性用于检索和设置筛选器 pin 的当前演示时间。

## <span id="ddk_ksproperty_stream_presentationtime_ks"></span><span id="DDK_KSPROPERTY_STREAM_PRESENTATIONTIME_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kstime" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kstime)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY \_ STREAM \_ PRESENTATIONTIME 是一个可选属性，如果 pin 保留位置信息，或在与界定闭合相关的 pin 之间使用不同的时间戳格式，则应该实现该属性。 因此，它需要在出现搜索表示时间时将时间戳转换为。

筛选器 pin 的显示时间指定为 [**KSTIME**](/windows-hardware/drivers/ddi/ks/ns-ks-kstime) 结构，其解释依赖于所使用的接口。 对于标准流式处理接口，时间以100毫微秒为增量 (，除非分子和分母另外指定) 表示该筛选器当前正在处理或正在寻找处理的流的表示位置。 如果这是渲染筛选器，此位置表示当前正在呈现的数据。 此位置信息与主时钟的显示时间同步。 呈现时间通常从零开始，并可能表示文件数据的时间偏移量。 可以使用分子和分母来指定接口强制执行的块对齐。

在转换搜索请求期间转换位置值时也使用此属性。 一个插针上的查找位置值在筛选器中转换为在界定闭合相关的 pin 上显示时间。 客户端使用新的流位置设置此属性，以便进行查找。 当在取消未完成的 i/o 并重置设备状态之后需要查找时，代理通常会调用此方法。 如果尚未执行重置，筛选器可能必须自动取消并正确重置。 将向属性传递一个 KSTIME，其中包含与连接所使用的接口一致的新流位置。

例如，在客户端 (后，DirectShow 代理) 会将查找请求写入一个连接，然后在显示时间查询其他界定闭合相关连接。 执行成功的读取请求的任何其他连接都会使代理将结果位置传递到该连接的另一端。 通过这种方式，在整个 DirectShow 图形) 中传播定位位置 (例如，无需知道客户端传递的初始单元格式之外的单位格式。 当位置信息在筛选器中通过拓扑传播时，将在筛选器中进行转换。 使用此间接方法是因为通信方法可能在图形中的各种筛选器之间受到限制，具体取决于它们所使用的接口。 设置新的查找位置时，必须可接受分子/分母对。

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


[**KSTIME**](/windows-hardware/drivers/ddi/ks/ns-ks-kstime)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

