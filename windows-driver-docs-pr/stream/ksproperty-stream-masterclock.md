---
title: KSPROPERTY\_STREAM\_MASTERCLOCK
description: KSPROPERTY\_STREAM\_MASTERCLOCK 属性是一个可选属性，如果 pin 使用或生成可用于同步的主时钟，则应该实现该属性。
ms.assetid: b8fb4d7b-e2e3-498c-9f76-4075d3ae0cb2
keywords:
- KSPROPERTY_STREAM_MASTERCLOCK 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_MASTERCLOCK
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49b2baac5c511e5a71a4024f3af80e1bab767b97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844954"
---
# <a name="ksproperty_stream_masterclock"></a>KSPROPERTY\_STREAM\_MASTERCLOCK


KSPROPERTY\_STREAM\_MASTERCLOCK 属性是一个可选属性，如果 pin 使用或生成可用于同步的主时钟，则应该实现该属性。

## <span id="ddk_ksproperty_stream_masterclock_ks"></span><span id="DDK_KSPROPERTY_STREAM_MASTERCLOCK_KS"></span>


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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>柄</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在查询时，属性返回**NULL**句柄。 支持取决于调用是否成功返回。

你可以使用 KSPROPERTY\_STREAM\_MASTERCLOCK 来查询某个 pin 是否支持某个主时钟，或者是否为 pin 设置当前的主时钟。 通常通过图形管理器（如在 DirectShow 中）完成此操作。 检索主时钟句柄并将其用于在另一个插针上设置主时钟，也可以将其用作主时钟的用户模式代理，如在 DirectShow 图形中。

如果在 pin 上设置时钟，则 pin 将引用基础文件对象，并可在以后对该文件对象执行查询。 文件句柄本身必须由查询该句柄的客户端关闭。

当筛选器既不生成主时钟也不需要引用一个时，筛选器不需要支持该属性，例如，在关系图中间放置的转换器筛选器无需与其他流同步。 如果筛选器生成了主时钟但不同步到外部主时钟，则该属性还可用作只读。

另请参阅[KS 时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)和[AVStream 时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-clocks)。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






