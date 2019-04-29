---
title: ScanTicket 元素
description: 所需的 ScanTicket 元素定义的所有当前标识的扫描作业的说明和处理的参数。
ms.assetid: d507bd46-8fc4-49d3-9575-2d83fd7ae625
keywords:
- ScanTicket 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5089696e6c40b81074dcb9e38d92a786e707610f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356216"
---
# <a name="scanticket-element"></a>ScanTicket 元素


所需**ScanTicket**元素定义的所有当前标识的扫描作业的说明和处理的参数。

<a name="usage"></a>用法
-----

```xml
<wscn:ScanTicket>
  child elements
</wscn:ScanTicket>
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>Job</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="validatescanticketrequest.md" data-raw-source="[&lt;strong&gt;ValidateScanTicketRequest&lt;/strong&gt;](validatescanticketrequest.md)"><strong>ValidateScanTicketRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScanTicket**元素包含客户端选择的当前作业的扫描程序设置的值。 客户端构造**ScanTicket**通过只在扫描仪支持这些值。 客户端通过调用获取此类值[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作和扫描程序的要求提供[ **DefaultScanTicket** ](defaultscanticket.md)元素。

成员元素**ScanTicket**映射到的实例直接[**作业**](job.md)元素，并且它们是完全客户端需要发送到扫描程序[ **CreateScanJobRequest** ](createscanjobrequest.md)操作。

客户端可以请求**ScanTicket**元素通过调用特定作业。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**DocumentParameters**](documentparameters.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**Job**](job.md)

[**JobDescription**](jobdescription.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

 

 






