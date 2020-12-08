---
title: RequestedElements 元素
description: 必需的 RequestedElements 元素用于标识客户端在调用 GetScannerElementsRequest 或 GetJobElementsRequest 时要获取的数据的元素。
keywords:
- RequestedElements 元素图像设备
topic_type:
- apiref
api_name:
- wscn RequestedElements
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2379923644838b1b886c5f8379b835411f497a4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793635"
---
# <a name="requestedelements-element"></a>RequestedElements 元素


必需的 **RequestedElements** 元素用于标识客户端在调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 或 [**GetJobElementsRequest**](getjobelementsrequest.md)时要获取的数据的元素。

<a name="usage"></a>使用情况
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
<td><p><a href="name-for-requestedelements-element.md" data-raw-source="[&lt;strong&gt;Name for RequestedElements Element&lt;/strong&gt;](name-for-requestedelements-element.md)"><strong>RequestedElements 元素的名称</strong></a></p></td>
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

**RequestedElements** 元素包含一个或多个 parent **RequestedElements** 元素的 **Name** 元素，这些元素用于标识客户端正在查询的数据。

## <a name="see-also"></a>请参阅


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**RequestedElements 元素的名称**](name-for-requestedelements-element.md)

 

 






