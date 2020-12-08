---
title: 宽度元素
description: 必需的宽度元素包含扫描程序可以扫描图像的宽度列表。
keywords:
- 宽度元素图像设备
topic_type:
- apiref
api_name:
- wscn Widths
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545503f32ba78481e692739007a0289c65f82d00
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826345"
---
# <a name="widths-element"></a>宽度元素


必需的 **宽度** 元素包含扫描程序可以扫描图像的宽度列表。

<a name="usage"></a>使用情况
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
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>宽度</strong></a></p></td>
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

每个 [**Width**](width.md) 元素都指定设备可以扫描图像的每英寸的有效水平像素数。

[**高度**](heights.md)元素包含扫描程序支持的高度的列表。

## <a name="see-also"></a>请参阅


[**ADFResolutions**](adfresolutions.md)

[**FilmResolutions**](filmresolutions.md)

[**高度**](height.md)

[**Heights**](heights.md)

[**PlatenResolutions**](platenresolutions.md)

[**宽度**](width.md)

 

 






