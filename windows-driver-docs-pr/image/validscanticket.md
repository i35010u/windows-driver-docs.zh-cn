---
title: ValidScanTicket 元素
description: 可选 ValidScanTicket 元素包含有效 ScanTicket。
ms.assetid: 306b5d90-068f-4b63-9155-8f35c7825f16
keywords:
- ValidScanTicket 元素成像设备
topic_type:
- apiref
api_name:
- wscn ValidScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8823a98372fc413a795177c9c5e8ed403a31cdb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356146"
---
# <a name="validscanticket-element"></a>ValidScanTicket 元素


可选**ValidScanTicket**元素中包含有效[ **ScanTicket**](scanticket.md)。

<a name="usage"></a>用法
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

客户端提交[ **ScanTicket** ](scanticket.md)通过验证[ **ValidateScanTicketRequest** ](validatescanticketrequest.md)操作。 如果提交**ScanTicket**包含无效的设置，必须返回 WSD 扫描服务**ValidScanTicket**元素已在其中更改任何无效的设置，以有效的设置。 扫描服务将返回验证信息，其中包括**ValidScanTicket**，在[ **ValidateScanTicketResponse**](validatescanticketresponse.md)。

## <a name="see-also"></a>请参阅


[**DocumentParameters**](documentparameters.md)

[**JobDescription**](jobdescription.md)

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

[**ValidationInfo**](validationinfo.md)

 

 






