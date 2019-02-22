---
title: DestinationResponses 元素
description: 所需的 DestinationResponses 元素是所有客户端的扫描目标请求的响应的集合。
ms.assetid: f373b584-eec9-412e-80b2-3d8a69f4b7ca
keywords:
- DestinationResponses 元素成像设备
topic_type:
- apiref
api_name:
- wscn DestinationResponses
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccb08fddbdba327c176428e2f4efffa3ba14d11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520943"
---
# <a name="destinationresponses-element"></a>DestinationResponses 元素


所需**DestinationResponses**元素是所有客户端的扫描目标请求的响应的集合。

<a name="usage"></a>用法
-----

```xml
<wscn:DestinationResponses>
  child elements
</wscn:DestinationResponses>
```

<a name="attributes"></a>属性
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
<td><p>&lt;wse:SubscribeResponse&gt;</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务必须指定一个[ **DestinationResponse** ](destinationresponse.md)中的子元素**DestinationResponses**元素为每个[ **ScanDestination** ](scandestination.md)客户端在指定的元素 **&lt;wse： 订阅&gt;** 请求。  **&lt;Wse： 订阅&gt;** 元素规范中所述。

## <a name="see-also"></a>另请参阅


[**DestinationResponse**](destinationresponse.md)

[**ScanDestination**](scandestination.md)

 

 






