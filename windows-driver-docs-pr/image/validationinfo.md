---
title: ValidationInfo 元素
description: 必需的 ValidationInfo 元素包含所有 ScanTicket 验证信息，以响应客户端的 ValidateScanTicketRequest。
keywords:
- ValidationInfo 元素图像设备
topic_type:
- apiref
api_name:
- wscn ValidationInfo
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1231960c9c2b733dce498b478a43563f6d829116
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815397"
---
# <a name="validationinfo-element"></a>ValidationInfo 元素


必需的 **ValidationInfo** 元素包含所有 [**ScanTicket**](scanticket.md) 验证信息，以响应客户端的 [**ValidateScanTicketRequest**](validatescanticketrequest.md)。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ValidationInfo>
  child elements
</wscn:ValidationInfo>
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
<td><p><a href="imageinformation.md" data-raw-source="[&lt;strong&gt;ImageInformation&lt;/strong&gt;](imageinformation.md)"><strong>ImageInformation</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="validscanticket.md" data-raw-source="[&lt;strong&gt;ValidScanTicket&lt;/strong&gt;](validscanticket.md)"><strong>ValidScanTicket</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="validticket.md" data-raw-source="[&lt;strong&gt;ValidTicket&lt;/strong&gt;](validticket.md)"><strong>ValidTicket</strong></a></p></td>
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
<td><p><a href="validatescanticketresponse.md" data-raw-source="[&lt;strong&gt;ValidateScanTicketResponse&lt;/strong&gt;](validatescanticketresponse.md)"><strong>ValidateScanTicketResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ValidationInfo** 元素包含定义客户端的 [**ScanTicket**](scanticket.md)是否有效的元素，如果不是，则 WSD 扫描服务更改的数据以使票证有效。 扫描服务会在其 [**ValidateScanTicketResponse**](validatescanticketresponse.md) 操作中返回此信息。

## <a name="see-also"></a>请参阅


[**ImageInformation**](imageinformation.md)

[**ScanTicket**](scanticket.md)

[**ValidScanTicket**](validscanticket.md)

[**ValidTicket**](validticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

 

 






