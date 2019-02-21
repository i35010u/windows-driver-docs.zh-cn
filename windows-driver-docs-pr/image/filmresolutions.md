---
title: FilmResolutions 元素
description: 所需的 FilmResolutions 元素包含一系列扫描输入的源的扫描程序的电影可以扫描的解决方法。
ms.assetid: a273ac11-e1ae-4329-a6a2-e47accf564a9
keywords:
- FilmResolutions 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cb24459bb3bd53047392984f96f786ac9cc2b13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554527"
---
# <a name="filmresolutions-element"></a>FilmResolutions 元素


所需**FilmResolutions**元素包含一系列扫描输入的源的扫描程序的电影可以扫描的解决方法。

<a name="usage"></a>用法
-----

```xml
<wscn:FilmResolutions>
  child elements
</wscn:FilmResolutions>
```

<a name="attributes"></a>属性
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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>高度</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="widths.md" data-raw-source="[&lt;strong&gt;Widths&lt;/strong&gt;](widths.md)"><strong>Widths</strong></a></p></td>
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>Film</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

解决方法指定为[**宽度**](width.md) x [**高度**](height.md)对，其中同时**宽度**和**高度**以每英寸点数的像素为单位指定。

WSD 扫描服务应列出扫描设备支持中的所有可能的宽度**宽度**子元素和扫描设备支持中的所有可能高度**高度**子元素。 所有**宽度**并**高度**的值为独立于彼此，和大多数设备将支持这些配对中的任意组合[ **ScanTicket**](scanticket.md)元素。

## <a name="see-also"></a>另请参阅


[**Film**](film.md)

[**Height**](height.md)

[**高度**](heights.md)

[**ScanTicket**](scanticket.md)

[**Width**](width.md)

[**Widths**](widths.md)

 

 






