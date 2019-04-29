---
title: DestinationToken 元素
description: 所需的 DestinationToken 元素包含扫描程序将分配给当前的客户端目标的特定于设备的字符串。
ms.assetid: 92ff99a2-079a-4001-aa01-ff5db09f6fd2
keywords:
- DestinationToken 元素成像设备
topic_type:
- apiref
api_name:
- wscn DestinationToken
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3c7643a90b37ff7993fdde5582883ef31cb0d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373182"
---
# <a name="destinationtoken-element"></a>DestinationToken 元素


所需**DestinationToken**元素包含为当前的客户端目标扫描程序分配一个特定于设备的字符串。

<a name="usage"></a>用法
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端包括**DestinationToken**令牌会在发送时[ **CreateScanJobRequest** ](createscanjobrequest.md)操作元素的后面[ **ScanAvailableEvent** ](scanavailableevent.md)事件。 WSD 扫描服务使用指定的字符串来检查正确的客户端发送扫描请求。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DestinationResponse**](destinationresponse.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






