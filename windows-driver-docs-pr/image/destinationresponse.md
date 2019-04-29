---
title: DestinationResponse 元素
description: 所需的 DestinationResponse 元素包含单个 ScanDestination 注册响应信息。
ms.assetid: 388304ca-4d62-40cf-ad68-13607a836caf
keywords:
- DestinationResponse 元素成像设备
topic_type:
- apiref
api_name:
- wscn DestinationResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43cf9feb3851452b48e97db1cefb9ec492eb649b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373196"
---
# <a name="destinationresponse-element"></a>DestinationResponse 元素


所需**DestinationResponse**元素包含的响应信息的单个[ **ScanDestination** ](scandestination.md)注册。

<a name="usage"></a>用法
-----

```xml
<wscn:DestinationResponse>
  child elements
</wscn:DestinationResponse>
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
<td><p>&lt;供应商定义的任何元素&gt;</p></td>
</tr>
<tr class="even">
<td><p><a href="clientcontext.md" data-raw-source="[&lt;strong&gt;ClientContext&lt;/strong&gt;](clientcontext.md)"><strong>ClientContext</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="destinationtoken.md" data-raw-source="[&lt;strong&gt;DestinationToken&lt;/strong&gt;](destinationtoken.md)"><strong>DestinationToken</strong></a></p></td>
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
<td><p><a href="destinationresponses.md" data-raw-source="[&lt;strong&gt;DestinationResponses&lt;/strong&gt;](destinationresponses.md)"><strong>DestinationResponses</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DestinationResponse**元素包含[ **ClientContext** ](clientcontext.md)元素从其匹配[ **ScanDestination**](scandestination.md)元素，以便客户端可以确定响应。 **DestinationResponse**还包含[ **DestinationToken** ](destinationtoken.md)元素用于所有[ **CreateScanJobRequest** ](createscanjobrequest.md)此目标中的操作元素。

## <a name="see-also"></a>请参阅


[**ClientContext**](clientcontext.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DestinationResponses**](destinationresponses.md)

[**DestinationToken**](destinationtoken.md)

[**ScanDestination**](scandestination.md)

 

 






