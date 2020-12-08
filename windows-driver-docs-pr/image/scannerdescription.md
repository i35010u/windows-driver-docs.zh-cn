---
title: ScannerDescription 元素
description: ScannerDescription 元素
keywords:
- ScannerDescription 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerDescription
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd3fb9e2a3056b84efcf771673bc9e128b023114
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815109"
---
# <a name="scannerdescription-element"></a>ScannerDescription 元素


<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerDescription>
  child elements
</wscn:ScannerDescription>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

无

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
<td><p><a href="scannerinfo.md" data-raw-source="[&lt;strong&gt;ScannerInfo&lt;/strong&gt;](scannerinfo.md)"><strong>ScannerInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerlocation.md" data-raw-source="[&lt;strong&gt;ScannerLocation&lt;/strong&gt;](scannerlocation.md)"><strong>ScannerLocation</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannername.md" data-raw-source="[&lt;strong&gt;ScannerName&lt;/strong&gt;](scannername.md)"><strong>ScannerName</strong></a></p></td>
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
<td><p><a href="elementchanges.md" data-raw-source="[&lt;strong&gt;ElementChanges&lt;/strong&gt;](elementchanges.md)"><strong>ElementChanges</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="elementdata-for-scannerelements-element.md" data-raw-source="[&lt;strong&gt;ElementData for parent ScannerElements&lt;/strong&gt;](elementdata-for-scannerelements-element.md)"><strong>ElementData for parent ScannerElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

**ScannerDescription** 元素包含有关很少或从不更改的扫描程序的信息。 客户端通过调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 操作元素来检索此信息。

## <a name="see-also"></a>请参阅


[**ElementChanges**](elementchanges.md)

[**ElementData for parent ScannerElements**](elementdata-for-scannerelements-element.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerInfo**](scannerinfo.md)

[**ScannerLocation**](scannerlocation.md)

[**ScannerName**](scannername.md)

 

 






