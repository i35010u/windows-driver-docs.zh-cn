---
title: ClientContext 元素
description: 必需的 ClientContext 元素指定特定于客户端的字符串。
keywords:
- ClientContext 元素图像处理设备
topic_type:
- apiref
api_name:
- wscn ClientDisplayName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d662af9e4038dde46cb58f3a1c2f3dbb96238aea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798177"
---
# <a name="clientcontext-element"></a>ClientContext 元素


必需的 **ClientContext** 元素指定特定于客户端的字符串。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ClientDisplayName>
  text
</wscn:ClientDisplayName>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 任何有效的字符串。

## <a name="child-elements"></a>子元素


没有任何子元素。

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

当 **clientcontext** 元素的父元素是 [**ScanDestination**](scandestination.md)时， **clientcontext** 指定客户端在 **&lt; wse：订阅 &gt;** 请求中提供的字符串值，接收 [**ScanAvailableEvent**](scanavailableevent.md)事件。

父元素为 [**DestinationResponse**](destinationresponse.md)时， **ClientContext** 是客户端在订阅操作中发送的数据的副本。 当 WSD 扫描服务响应客户端的订阅请求时，它会在 **&lt; Wse： SubscribeResponse &gt;** 中返回此副本。

当父元素为 [**ScanAvailableEvent**](scanavailableevent.md)时， **ClientContext** 包含扫描器作为 **ScanAvailableEvent** 订阅请求一部分接收的字符串值。 此字符串使客户端可以将 **ScanAvailableEvent** 与正确的扫描程序设备和服务相关联。

在规范中介绍了 **&lt; Wse：订阅 &gt;** 和 **&lt; wse： SubscribeResponse &gt;** 元素。

## <a name="see-also"></a>请参阅


[**DestinationResponse**](destinationresponse.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






