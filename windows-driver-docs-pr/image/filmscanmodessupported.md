---
title: FilmScanModesSupported 元素
description: 必需的 FilmScanModesSupported 元素包含电影扫描选项支持的电影曝光类型的列表。
keywords:
- FilmScanModesSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn FilmScanModesSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: daff766ec39dac2d3a90b22464ea4c1c85e4f237
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808271"
---
# <a name="filmscanmodessupported-element"></a>FilmScanModesSupported 元素


必需的 **FilmScanModesSupported** 元素包含电影扫描选项支持的电影曝光类型的列表。

<a name="usage"></a>使用情况
-----

```xml
<wscn:FilmScanModesSupported>
  child elements
</wscn:FilmScanModesSupported>
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
<td><p><a href="filmscanmodevalue.md" data-raw-source="[&lt;strong&gt;FilmScanModeValue&lt;/strong&gt;](filmscanmodevalue.md)"><strong>FilmScanModeValue</strong></a></p></td>
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

**FilmScanModesSupported** 元素包含一个或多个 [**FilmScanModeValue**](filmscanmodevalue.md)子元素。 每个 **FilmScanModeValue** 元素标识胶卷扫描选项支持的电影曝光类型。

## <a name="see-also"></a>请参阅


[**胶片**](film.md)

[**FilmScanModeValue**](filmscanmodevalue.md)

 

 






