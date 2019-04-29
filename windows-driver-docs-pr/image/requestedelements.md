---
title: RequestedElements 元素
description: 所需的 RequestedElements 元素标识的客户端调用 GetScannerElementsRequest 或 GetJobElementsRequest 时需要的数据元素。
ms.assetid: 0023afc1-723d-4b6a-9f1a-0bc21a309a65
keywords:
- RequestedElements 元素成像设备
topic_type:
- apiref
api_name:
- wscn RequestedElements
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414b47dd5bf9aadf6beb7d9c4056d23bdfa4002c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367005"
---
# <a name="requestedelements-element"></a>RequestedElements 元素


所需**RequestedElements**元素标识的客户端希望当调用的数据元素[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)或[**GetJobElementsRequest**](getjobelementsrequest.md)。

<a name="usage"></a>用法
-----

```xml
<wscn:RequestedElements>
  child elements
</wscn:RequestedElements>
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
<td><p><a href="name-for-requestedelements-element.md" data-raw-source="[&lt;strong&gt;Name for RequestedElements Element&lt;/strong&gt;](name-for-requestedelements-element.md)"><strong>RequestedElements 元素名称</strong></a></p></td>
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
<td><p><a href="getjobelementsrequest.md" data-raw-source="[&lt;strong&gt;GetJobElementsRequest&lt;/strong&gt;](getjobelementsrequest.md)"><strong>GetJobElementsRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="getscannerelementsrequest.md" data-raw-source="[&lt;strong&gt;GetScannerElementsRequest&lt;/strong&gt;](getscannerelementsrequest.md)"><strong>GetScannerElementsRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**RequestedElements**元素包含一个或多个**名称**元素的父**RequestedElements**标识查询客户端的数据的元素。

## <a name="see-also"></a>请参阅


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**RequestedElements 元素名称**](name-for-requestedelements-element.md)

 

 






