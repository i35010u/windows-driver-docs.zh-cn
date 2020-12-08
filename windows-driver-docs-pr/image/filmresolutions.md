---
title: FilmResolutions 元素
description: 必需的 FilmResolutions 元素包含一个解决方案列表，扫描程序的电影扫描输入源可以在此列表中扫描。
keywords:
- FilmResolutions 元素图像设备
topic_type:
- apiref
api_name:
- wscn FilmResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07c23ea9c4a3e86ef7b79f815dc403f1f93c563e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808273"
---
# <a name="filmresolutions-element"></a>FilmResolutions 元素


必需的 **FilmResolutions** 元素包含一个解决方案列表，扫描程序的电影扫描输入源可以在此列表中扫描。

<a name="usage"></a>使用情况
-----

```xml
<wscn:FilmResolutions>
  child elements
</wscn:FilmResolutions>
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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>Heights</strong></a></p></td>
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>胶片</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

分辨率指定为 [**宽度**](width.md) x [**高度**](height.md) 对，其中的 **宽度** 和 **高度** 均以每英寸像素数来指定。

WSD 扫描服务应列出扫描设备支持的 **宽度** 子元素中的所有可能宽度，以及扫描设备支持的 **高度** 子元素中的所有可能的高度。 所有的 **宽度** 和 **高度** 值都彼此独立，并且大多数设备将支持在 [**ScanTicket**](scanticket.md) 元素内的任何组合中配对它们。

## <a name="see-also"></a>请参阅


[**胶片**](film.md)

[**高度**](height.md)

[**Heights**](heights.md)

[**ScanTicket**](scanticket.md)

[**宽度**](width.md)

[**Widths**](widths.md)

 

 






