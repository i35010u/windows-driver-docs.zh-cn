---
title: DestinationResponses 元素
description: 必需的 DestinationResponses 元素是对客户端扫描目标请求的所有响应的集合。
keywords:
- DestinationResponses 元素图像设备
topic_type:
- apiref
api_name:
- wscn DestinationResponses
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea576a5944523580b8c9f8582230363b9d462291
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838597"
---
# <a name="destinationresponses-element"></a>DestinationResponses 元素


必需的 **DestinationResponses** 元素是对客户端扫描目标请求的所有响应的集合。

<a name="usage"></a>使用情况
-----

```xml
<wscn:DestinationResponses>
  child elements
</wscn:DestinationResponses>
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
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
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
<td><p>&lt;wse： SubscribeResponse&gt;</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

对于客户端在 **&lt; &gt; wse：订阅** 请求中指定的每个 [**ScanDestination**](scandestination.md)元素，WSD 扫描服务必须在 **DestinationResponses** 元素中指定一个 [**DestinationResponse**](destinationresponse.md)子元素。 **&lt; Wse：订阅 &gt;** 元素在规范中进行了介绍。

## <a name="see-also"></a>请参阅


[**DestinationResponse**](destinationresponse.md)

[**ScanDestination**](scandestination.md)

 

 






