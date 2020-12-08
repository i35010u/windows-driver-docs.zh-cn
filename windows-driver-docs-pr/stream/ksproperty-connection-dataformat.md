---
title: KSPROPERTY \_ 连接 \_ DATAFORMAT
description: 客户端使用 KSPROPERTY \_ 连接 \_ DATAFORMAT 属性设置当前数据格式。
keywords:
- KSPROPERTY_CONNECTION_DATAFORMAT 流媒体设备
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
ms.openlocfilehash: 587fbc89d79c2b2cbb59d6cab4454f4f8180dec7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803457"
---
# <a name="ksproperty_connection_dataformat"></a>KSPROPERTY \_ 连接 \_ DATAFORMAT


客户端使用 KSPROPERTY \_ 连接 \_ DATAFORMAT 属性设置当前数据格式。

## <span id="ddk_ksproperty_connection_dataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_DATAFORMAT_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性采用 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 结构来指定所请求的数据格式。

如果 KS 筛选器允许客户端重置当前属性，或如果无法以未完全指定的数据格式进行连接，则该筛选器只需支持此属性。

有关 KSPROPERTY \_ CONNECTION DATAFORMAT 属性的详细信息 \_ ，请参阅 [KS 数据格式和数据范围](./ks-data-formats-and-data-ranges.md) 和 [AVStream 中的数据范围交集](./data-range-intersections-in-avstream.md)。

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

## <a name="see-also"></a>请参阅


[**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)

[**KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

