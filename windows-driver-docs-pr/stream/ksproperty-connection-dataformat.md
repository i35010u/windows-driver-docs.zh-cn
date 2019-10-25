---
title: KSPROPERTY\_连接\_DATAFORMAT
description: 客户端使用 KSPROPERTY\_连接\_DATAFORMAT 属性来设置当前数据格式。
ms.assetid: c5f37f1b-7dc6-46d2-aba2-b6c03f07228d
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
ms.openlocfilehash: 5aa1e35d2ecf6fe5d855f7a3e24c84af6543d404
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826798"
---
# <a name="ksproperty_connection_dataformat"></a>KSPROPERTY\_连接\_DATAFORMAT


客户端使用 KSPROPERTY\_连接\_DATAFORMAT 属性来设置当前数据格式。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性采用[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构来指定所请求的数据格式。

如果 KS 筛选器允许客户端重置当前属性，或如果无法以未完全指定的数据格式进行连接，则该筛选器只需支持此属性。

有关 KSPROPERTY\_连接\_DATAFORMAT 属性的详细信息，请参阅[KS 数据格式和](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges) [AVStream 中](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)的数据范围交集。

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


[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)

[**KSPROPERTY\_连接\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

 

 






