---
title: 宽度元素
description: 所需的宽度元素列出的扫描程序扫描图像的宽度。
ms.assetid: 785d469f-bdad-413c-8bfb-de7a518b243c
keywords:
- 宽度元素成像设备
topic_type:
- apiref
api_name:
- wscn Widths
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ff2d7262c2c30be8827726630c83e8f4fdd0afe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380231"
---
# <a name="widths-element"></a>宽度元素


所需**宽度**元素包含扫描程序扫描图像的宽度的列表。

<a name="usage"></a>用法
-----

```xml
<wscn:Widths>
  child elements
</wscn:Widths>
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
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>Width</strong></a></p></td>
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

每个[**宽度**](width.md)子元素指定为有效的每英寸点数设备扫描图像的水平像素数。

[**高度**](heights.md)元素包含在扫描仪支持的具有高度的列表。

## <a name="see-also"></a>请参阅


[**ADFResolutions**](adfresolutions.md)

[**FilmResolutions**](filmresolutions.md)

[**Height**](height.md)

[**高度**](heights.md)

[**PlatenResolutions**](platenresolutions.md)

[**Width**](width.md)

 

 






