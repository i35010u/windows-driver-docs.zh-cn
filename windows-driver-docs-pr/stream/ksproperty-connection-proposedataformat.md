---
title: KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT
description: 客户端可以使用 KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT 属性为连接建议新的数据格式。
ms.assetid: f5bc7cd2-0033-4761-962b-33c82925134b
keywords:
- KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f367ae0b49bbe5f31a586a66356ad43e10cf46b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102764"
---
# <a name="ksproperty_connection_proposedataformat"></a>KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT


客户端可以使用 KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT 属性为连接建议新的数据格式。

## <span id="ddk_ksproperty_connection_proposedataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT_KS"></span>


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

此属性返回指定建议数据格式的 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 。

\_如果可以将 pin 重置为建议的数据格式，则 KS 筛选器返回状态 "成功"; 否则返回错误代码。 请注意，此属性请求不会更改数据格式。 客户端使用 [**KSPROPERTY \_ 连接 \_ DATAFORMAT**](ksproperty-connection-dataformat.md) 来更改格式。

另请参阅 [KS 数据格式和数据区域](./ks-data-formats-and-data-ranges.md)。

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


[**KSPROPERTY \_ 连接 \_ DATAFORMAT**](ksproperty-connection-dataformat.md)

[*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)

