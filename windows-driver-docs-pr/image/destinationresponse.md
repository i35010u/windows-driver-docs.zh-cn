---
title: DestinationResponse 元素
description: 必需的 DestinationResponse 元素包含单个 ScanDestination 注册的响应信息。
keywords:
- DestinationResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn DestinationResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05dfb1f11ceff04b7705194cdb269ef136a118be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838599"
---
# <a name="destinationresponse-element"></a>DestinationResponse 元素


必需的 **DestinationResponse** 元素包含单个 [**ScanDestination**](scandestination.md) 注册的响应信息。

<a name="usage"></a>使用情况
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
<td><p>&lt;任何供应商定义的元素&gt;</p></td>
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

**DestinationResponse** 元素包含其匹配的 [**ScanDestination**](scandestination.md)元素中的 [**ClientContext**](clientcontext.md)元素，以便客户端可以标识响应。 **DestinationResponse** 还包含 [**DestinationToken**](destinationtoken.md) 元素，可在此目标的所有 [**CreateScanJobRequest**](createscanjobrequest.md) 操作元素中使用。

## <a name="see-also"></a>请参阅


[**ClientContext**](clientcontext.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DestinationResponses**](destinationresponses.md)

[**DestinationToken**](destinationtoken.md)

[**ScanDestination**](scandestination.md)

 

 






