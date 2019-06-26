---
title: KSPROPERTY\_连接\_DATAFORMAT
description: 客户端使用 KSPROPERTY\_连接\_DATAFORMAT 属性来设置当前的数据格式。
ms.assetid: c5f37f1b-7dc6-46d2-aba2-b6c03f07228d
keywords:
- KSPROPERTY_CONNECTION_DATAFORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_DATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22f64c5341e9a3a57d08d807c3cf558de1313f00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373117"
---
# <a name="kspropertyconnectiondataformat"></a>KSPROPERTY\_连接\_DATAFORMAT


客户端使用 KSPROPERTY\_连接\_DATAFORMAT 属性来设置当前的数据格式。

## <span id="ddk_ksproperty_connection_dataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_DATAFORMAT_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性采用[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)结构，它指定请求的数据格式。

只需支持此属性，如果它们允许客户端进行重置当前的属性，或者如果连接可以使用未完全指定的数据格式进行 KS 筛选器。

详细了解 KSPROPERTY\_连接\_DATAFORMAT 属性，请参阅[KS 数据格式和数据范围](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)和[AVStream 中的数据范围交集](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)。

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


[**KSSTREAM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)

[**KSPROPERTY\_CONNECTION\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

 

 






