---
title: ValidationInfo 元素
description: 所需的 ValidationInfo 元素包含对客户端的 ValidateScanTicketRequest 响应中的所有 ScanTicket 验证信息。
ms.assetid: c727cbd7-6da0-4750-b36e-3b65e56015fa
keywords:
- ValidationInfo 元素成像设备
topic_type:
- apiref
api_name:
- wscn ValidationInfo
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c6dd42552ec29116bdcd47a0bea3117c4c7b012
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354862"
---
# <a name="validationinfo-element"></a>ValidationInfo 元素


所需**ValidationInfo**元素包含所有[ **ScanTicket** ](scanticket.md)客户端的响应的验证信息[ **ValidateScanTicketRequest**](validatescanticketrequest.md)。

<a name="usage"></a>用法
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

**ValidationInfo**元素包含定义的元素是否在客户端[ **ScanTicket** ](scanticket.md)有效并且，如果不是，WSD 扫描服务更改，以使哪些数据有效的票证。 扫描服务将返回此信息在其[ **ValidateScanTicketResponse** ](validatescanticketresponse.md)操作。

## <a name="see-also"></a>请参阅


[**ImageInformation**](imageinformation.md)

[**ScanTicket**](scanticket.md)

[**ValidScanTicket**](validscanticket.md)

[**ValidTicket**](validticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

 

 






