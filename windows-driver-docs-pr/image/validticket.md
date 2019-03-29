---
title: ValidTicket 元素
description: 所需的 ValidTicket 元素指示客户端的 ScanTicket 是否有效。
ms.assetid: 8c2f35b5-1b1e-49a4-8aab-4d57ff9f1803
keywords:
- ValidTicket 元素成像设备
topic_type:
- apiref
api_name:
- wscn ValidTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62cce5fb77d4c10f1da4d1ea5c23129cba95c512
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576785"
---
# <a name="validticket-element"></a>ValidTicket 元素


所需**ValidTicket**元素指示客户端是否[ **ScanTicket** ](scanticket.md)有效。

<a name="usage"></a>用法
-----

```xml
<wscn:ValidTicket>
  text
</wscn:ValidTicket>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 一个布尔值，必须为 0，为 false，1 或 true。

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端提交[ **ScanTicket** ](scanticket.md)通过验证[ **ValidateScanTicketRequest** ](validatescanticketrequest.md)操作。 WSD 扫描服务将返回验证信息，其中包括**ValidTicket**，在[ **ValidateScanTicketResponse**](validatescanticketresponse.md)。

## <a name="see-also"></a>请参阅


[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

[**ValidationInfo**](validationinfo.md)

 

 






