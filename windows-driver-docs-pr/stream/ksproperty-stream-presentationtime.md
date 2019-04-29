---
title: KSPROPERTY\_流\_PRESENTATIONTIME
description: KSPROPERTY\_流\_PRESENTATIONTIME 属性用于检索和设置的筛选器 pin 当前的呈现时间。
ms.assetid: fb7bcd04-e600-4bab-b7e7-2b99e2bc0a6c
keywords:
- KSPROPERTY_STREAM_PRESENTATIONTIME 流式处理媒体设备
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
ms.openlocfilehash: 0bf4e8ff2598abc3b75d14ca98631314f40603b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379958"
---
# <a name="kspropertystreampresentationtime"></a>KSPROPERTY\_流\_PRESENTATIONTIME


KSPROPERTY\_流\_PRESENTATIONTIME 属性用于检索和设置的筛选器 pin 当前的呈现时间。

## <span id="ddk_ksproperty_stream_presentationtime_ks"></span><span id="DDK_KSPROPERTY_STREAM_PRESENTATIONTIME_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567145" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567145)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_流\_PRESENTATIONTIME 是可选属性，如果 pin 将保留位置信息或与不同的时间戳格式在拓扑结构上使用不同的接口应实现相关的 pin。 因此，它需具有时间戳转换发生时查找呈现时间。

筛选器 pin 的呈现时间指定为[ **KSTIME** ](https://msdn.microsoft.com/library/windows/hardware/ff567145)结构的解释取决于所用的接口。 对于标准流式处理接口，指定的时间以 100 纳秒的增量 （除非分子和分母另有指定） 表示的筛选器的流表示位置的当前正在处理或查找来处理。 如果这是呈现筛选器，此位置将表示当前正在呈现的数据。 此定位信息与主时钟的呈现时间同步。 呈现时间通常从零开始，并可能表示为文件数据的时间偏移量。 分子和分母可以用于指定界面强制实施的块对齐方式。

转换期间的查找请求传播的位置值时，还使用此属性。 在一个插针上的查找位置值将转换到拓扑结构上相关的插针上的呈现时间筛选器内。 客户端才能查找设置此属性与新的流位置。 这通常称为代理后，取消未完成 i/o 操作和重置设备状态需要搜寻时。 如果尚未执行重置，筛选器可能需要自动取消并相应地重置。 包含与该连接上使用的接口相一致的单位中的新流位置 KSTIME 被传入的属性。

客户端 （例如，DirectShow 代理） 将查找请求写入到一个连接后，然后针对呈现时间查询其他拓扑结构上相关的连接。 执行成功的读取的请求的任何其他连接使代理将结果位置传递给该连接的另一端。 以这种方式，查找位置 （例如，在 DirectShow 图） 会传播而无需知道传递客户端的初始单元格式之外的单位格式。 翻译出现在筛选器，如通过筛选器中的拓扑进行传播的位置信息。 因为通信方法可能会受到限制，具体取决于它们使用的接口图中的各种筛选器之间使用此间接方法。 当设置新的查找位置，分子/分母对必须是可以接受的 pin。

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


[**KSTIME**](https://msdn.microsoft.com/library/windows/hardware/ff567145)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






