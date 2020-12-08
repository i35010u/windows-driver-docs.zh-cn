---
title: ScanTicket 元素
description: 必需的 ScanTicket 元素定义当前标识的扫描作业的所有说明和处理参数。
keywords:
- ScanTicket 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdb2c00ff862660c41513a3bd6b2ad65fb222d7e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839103"
---
# <a name="scanticket-element"></a>ScanTicket 元素


必需的 **ScanTicket** 元素定义当前标识的扫描作业的所有说明和处理参数。

<a name="usage"></a>使用情况
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>作业</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="validatescanticketrequest.md" data-raw-source="[&lt;strong&gt;ValidateScanTicketRequest&lt;/strong&gt;](validatescanticketrequest.md)"><strong>ValidateScanTicketRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScanTicket** 元素包含客户端选择的当前作业的扫描程序设置的值。 客户端仅使用 scanner 支持的那些值构造 **ScanTicket** 。 客户端通过调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 操作获取此类值，并请求扫描仪的 [**DefaultScanTicket**](defaultscanticket.md) 元素。

**ScanTicket** 的成员元素直接映射到 [**作业**](job.md)元素的实例，并且它们正是客户端在 [**CreateScanJobRequest**](createscanjobrequest.md)操作过程中需要发送到扫描程序的内容。

客户端可以通过调用来请求特定作业的 **ScanTicket** 元素。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**DocumentParameters**](documentparameters.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**作业**](job.md)

[**JobDescription**](jobdescription.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

 

 






