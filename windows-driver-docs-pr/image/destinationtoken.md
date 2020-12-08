---
title: DestinationToken 元素
description: 必需的 DestinationToken 元素包含扫描程序分配给当前客户端目标的设备特定字符串。
keywords:
- DestinationToken 元素图像设备
topic_type:
- apiref
api_name:
- wscn DestinationToken
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8810b9f11e2098c3b8fa8991d6a58a77c0135c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838595"
---
# <a name="destinationtoken-element"></a>DestinationToken 元素


必需的 **DestinationToken** 元素包含扫描程序分配给当前客户端目标的设备特定字符串。

<a name="usage"></a>使用情况
-----

```xml
<wscn:DestinationToken>
  text
</wscn:DestinationToken>
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当客户端在 [**ScanAvailableEvent**](scanavailableevent.md)事件后发送 [**CreateScanJobRequest**](createscanjobrequest.md)操作元素时，将包括 **DestinationToken** 标记。 WSD 扫描服务使用指定的字符串来检查正确的客户端是否正在发送扫描请求。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DestinationResponse**](destinationresponse.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






