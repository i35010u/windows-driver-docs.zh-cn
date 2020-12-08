---
title: 高度元素
description: 必需的高度元素包含扫描程序可以扫描图像的高度的列表。
keywords:
- 高度元素图像设备
topic_type:
- apiref
api_name:
- wscn Heights
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e266906a0c2bbaf68ea18d898d155b4b80fbc9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793743"
---
# <a name="heights-element"></a>高度元素


必需的 **高度** 元素包含扫描程序可以扫描图像的高度的列表。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Heights>
  child elements
</wscn:Heights>
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>高度</strong></a></p></td>
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
<td><p><a href="adfresolutions.md" data-raw-source="[&lt;strong&gt;ADFResolutions&lt;/strong&gt;](adfresolutions.md)"><strong>ADFResolutions</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmresolutions.md" data-raw-source="[&lt;strong&gt;FilmResolutions&lt;/strong&gt;](filmresolutions.md)"><strong>FilmResolutions</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenresolutions.md" data-raw-source="[&lt;strong&gt;PlatenResolutions&lt;/strong&gt;](platenresolutions.md)"><strong>PlatenResolutions</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

每个 [**Height**](height.md) 子元素指定设备可以扫描图像的每英寸的有效垂直像素数。

[**宽度**](widths.md)元素包含扫描仪支持的宽度列表。

## <a name="see-also"></a>请参阅


[**ADFResolutions**](adfresolutions.md)

[**FilmResolutions**](filmresolutions.md)

[**高度**](height.md)

[**PlatenResolutions**](platenresolutions.md)

[**宽度**](width.md)

[**Widths**](widths.md)

 

 






