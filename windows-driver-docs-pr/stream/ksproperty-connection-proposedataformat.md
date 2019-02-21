---
title: KSPROPERTY\_CONNECTION\_PROPOSEDATAFORMAT
description: 客户端可以使用 KSPROPERTY\_连接\_PROPOSEDATAFORMAT 属性来提出新的数据格式的连接。
ms.assetid: f5bc7cd2-0033-4761-962b-33c82925134b
keywords:
- KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT 流式处理媒体设备
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
ms.openlocfilehash: d8cd31fbb4ee42bf5b86e95866d12c38d66d85ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544535"
---
# <a name="kspropertyconnectionproposedataformat"></a>KSPROPERTY\_CONNECTION\_PROPOSEDATAFORMAT


客户端可以使用 KSPROPERTY\_连接\_PROPOSEDATAFORMAT 属性来提出新的数据格式的连接。

## <span id="ddk_ksproperty_connection_proposedataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)指定建议的数据格式。

KS 筛选器将返回状态\_如果 pin 可以重置为建议的数据格式或错误代码否则成功。 请注意，此属性请求不会更改数据格式。 客户端使用[ **KSPROPERTY\_连接\_DATAFORMAT** ](ksproperty-connection-dataformat.md)更改的格式。

另请参阅[KS 数据格式和数据范围](https://msdn.microsoft.com/library/windows/hardware/ff567632)。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_连接\_DATAFORMAT**](ksproperty-connection-dataformat.md)

[*AVStrMiniPinSetDataFormat*](https://msdn.microsoft.com/library/windows/hardware/ff556355)

 

 






