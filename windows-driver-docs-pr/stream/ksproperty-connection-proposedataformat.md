---
title: KSPROPERTY\_连接\_PROPOSEDATAFORMAT
description: 客户端可以使用 KSPROPERTY\_连接\_PROPOSEDATAFORMAT 属性为连接建议新的数据格式。
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
ms.openlocfilehash: 46f00feeaf41cf15ce145b3deeafcffef7a4998d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826785"
---
# <a name="ksproperty_connection_proposedataformat"></a>KSPROPERTY\_连接\_PROPOSEDATAFORMAT


客户端可以使用 KSPROPERTY\_连接\_PROPOSEDATAFORMAT 属性为连接建议新的数据格式。

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

此属性返回指定建议数据格式的[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 。

如果可以将 pin 重置为建议的数据格式，则 KS 筛选器将返回状态\_成功; 否则返回错误代码。 请注意，此属性请求不会更改数据格式。 客户端使用[**KSPROPERTY\_连接\_DATAFORMAT**](ksproperty-connection-dataformat.md)来更改格式。

另请参阅[KS 数据格式和数据区域](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)。

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


[**KSPROPERTY\_连接\_DATAFORMAT**](ksproperty-connection-dataformat.md)

[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)

 

 






