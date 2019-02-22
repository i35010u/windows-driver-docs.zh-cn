---
title: ClientContext 元素
description: 所需的 ClientContext 元素指定特定于客户端的字符串。
ms.assetid: 09bc5f5b-6198-4553-9f6f-8219e620f634
keywords:
- ClientContext 元素成像设备
topic_type:
- apiref
api_name:
- wscn ClientDisplayName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 066bcbcfd99348610b9c2dd1b41bf0ca8d5b916d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540415"
---
# <a name="clientcontext-element"></a>ClientContext 元素


所需**ClientContext**元素指定特定于客户端的字符串。

<a name="usage"></a>用法
-----

```xml
<wscn:ClientDisplayName>
  text
</wscn:ClientDisplayName>
```

<a name="attributes"></a>属性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 任何有效字符的字符串。

## <a name="child-elements"></a>子元素


没有子元素。

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
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanavailableevent.md" data-raw-source="[&lt;strong&gt;ScanAvailableEvent&lt;/strong&gt;](scanavailableevent.md)"><strong>ScanAvailableEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当父元素的**ClientContext**元素是[ **ScanDestination**](scandestination.md)， **ClientContext**指定的字符串值客户端提供期间 **&lt;wse： 订阅&gt;** 接收请求[ **ScanAvailableEvent** ](scanavailableevent.md)事件。

当父元素是[ **DestinationResponse**](destinationresponse.md)， **ClientContext**是客户端订阅操作中发送的数据的副本。 WSD 扫描服务将返回在此副本**&lt;wse:SubscribeResponse&gt;** 时响应客户端的订阅请求。

当父元素是[ **ScanAvailableEvent**](scanavailableevent.md)， **ClientContext**包含字符串值作为的一部分收到的扫描程序**ScanAvailableEvent**订阅请求。 此字符串，客户端可以将相关联**ScanAvailableEvent**使用正确的扫描仪设备和服务。

 **&lt;Wse： 订阅&gt;** 并**&lt;wse:SubscribeResponse&gt;** 在规范中描述的元素。

## <a name="see-also"></a>另请参阅


[**DestinationResponse**](destinationresponse.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






