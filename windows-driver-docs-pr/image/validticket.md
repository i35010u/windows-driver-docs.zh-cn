---
title: ValidTicket 元素
description: 必需的 ValidTicket 元素指示客户端的 ScanTicket 是否有效。
keywords:
- ValidTicket 元素图像设备
topic_type:
- apiref
api_name:
- wscn ValidTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 811552a596d53106aec1253a0ac19b6f50713c84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832357"
---
# <a name="validticket-element"></a>ValidTicket 元素


必需的 **ValidTicket** 元素指示客户端的 [**ScanTicket**](scanticket.md) 是否有效。

<a name="usage"></a>使用情况
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

必需。 必须为0、false、1或 true 的布尔值。

## <a name="child-elements"></a>子元素


没有任何子元素。

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

客户端通过 [**ValidateScanTicketRequest**](validatescanticketrequest.md)操作提交 [**ScanTicket**](scanticket.md)进行验证。 WSD 扫描服务在 [**ValidateScanTicketResponse**](validatescanticketresponse.md)中返回验证信息，其中包括 **ValidTicket**。

## <a name="see-also"></a>请参阅


[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

[**ValidationInfo**](validationinfo.md)

 

 






