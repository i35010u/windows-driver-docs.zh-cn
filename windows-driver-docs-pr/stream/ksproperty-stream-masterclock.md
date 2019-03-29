---
title: KSPROPERTY\_STREAM\_MASTERCLOCK
description: KSPROPERTY\_流\_MASTERCLOCK 属性是可选属性，如果 pin 使用或生成可用于同步主时钟应实现。
ms.assetid: b8fb4d7b-e2e3-498c-9f76-4075d3ae0cb2
keywords:
- KSPROPERTY_STREAM_MASTERCLOCK 流式处理媒体设备
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
ms.openlocfilehash: e28352e9ec00e646771f26f6bf7df10e6b467f24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562382"
---
# <a name="kspropertystreammasterclock"></a>KSPROPERTY\_STREAM\_MASTERCLOCK


KSPROPERTY\_流\_MASTERCLOCK 属性是可选属性，如果 pin 使用或生成可用于同步主时钟应实现。

## <span id="ddk_ksproperty_stream_masterclock_ks"></span><span id="DDK_KSPROPERTY_STREAM_MASTERCLOCK_KS"></span>


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
<td><p>句柄</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

该属性返回**NULL**处理查询时。 通过调用是否成功返回确定支持。

可以使用 KSPROPERTY\_流\_MASTERCLOCK 查询主时钟是否受 pin 或设置一个 pin 的当前主时钟。 这通常是通过 graph 管理器中，如 DirectShow 中。 主时钟句柄检索并可用于在另一个插针上设置主时钟或可作为用户模式下代理的主时钟，如 DirectShow 关系图中。

时钟是设置 pin，pin 引用基础文件对象，并且可以更高版本执行针对该文件对象的查询。 必须由的客户端的查询的句柄关闭自身的文件句柄。

筛选器不支持属性时它既不会生成主时钟也不需要引用一个，如转换器筛选器放置而无需将与其他流同步图的中间。 该属性还可为只读时筛选器生成主时钟，但不会同步到外部的主时钟。

另请参阅[KS 时钟](https://msdn.microsoft.com/library/windows/hardware/ff567307)并[AVStream 时钟](https://msdn.microsoft.com/library/windows/hardware/ff554208)。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






