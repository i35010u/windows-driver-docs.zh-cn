---
title: ValidScanTicket 元素
description: 可选的 ValidScanTicket 元素包含有效的 ScanTicket。
keywords:
- ValidScanTicket 元素图像设备
topic_type:
- apiref
api_name:
- wscn ValidScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280fa515088fded8dce583eec77247b073b041a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815393"
---
# <a name="validscanticket-element"></a>ValidScanTicket 元素


可选的 **ValidScanTicket** 元素包含有效的 [**ScanTicket**](scanticket.md)。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ValidScanTicket>
  child elements
</wscn:ValidScanTicket>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


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
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
</tr>
</tbody>
</table>

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

客户端通过 [**ValidateScanTicketRequest**](validatescanticketrequest.md)操作提交 [**ScanTicket**](scanticket.md)进行验证。 如果提交的 **ScanTicket** 包含无效设置，则 WSD 扫描服务必须返回 **ValidScanTicket** 元素，在该元素中，它将任何无效的设置更改为有效设置。 扫描服务在 [**ValidateScanTicketResponse**](validatescanticketresponse.md)中返回验证信息，其中包括 **ValidScanTicket**。

## <a name="see-also"></a>请参阅


[**DocumentParameters**](documentparameters.md)

[**JobDescription**](jobdescription.md)

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

[**ValidationInfo**](validationinfo.md)

 

 






