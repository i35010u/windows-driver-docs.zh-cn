---
title: ScannerDescription 元素
description: ScannerDescription 元素
ms.assetid: 4429702e-18de-4b7c-83a2-ac405517e730
keywords:
- ScannerDescription 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerDescription
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbc371b4b0eb3b8f923f3dda3837ee9321685e73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370053"
---
# <a name="scannerdescription-element"></a>ScannerDescription 元素


<a name="usage"></a>用法
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
<td><p><a href="elementdata-for-scannerelements-element.md" data-raw-source="[&lt;strong&gt;ElementData for parent ScannerElements&lt;/strong&gt;](elementdata-for-scannerelements-element.md)"><strong>对于父 ScannerElements ElementData</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

**ScannerDescription**元素包含很少或从不进行更改的扫描程序有关的信息。 在客户端检索此信息通过调用[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作元素。

## <a name="see-also"></a>请参阅


[**ElementChanges**](elementchanges.md)

[**对于父 ScannerElements ElementData**](elementdata-for-scannerelements-element.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerInfo**](scannerinfo.md)

[**ScannerLocation**](scannerlocation.md)

[**ScannerName**](scannername.md)

 

 






