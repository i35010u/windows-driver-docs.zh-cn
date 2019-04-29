---
title: FilmScanModesSupported 元素
description: 所需的 FilmScanModesSupported 元素包含电影胶片扫描选项支持的公开类型的列表。
ms.assetid: bcc1335f-4465-4bc1-a804-b6e8729ec616
keywords:
- FilmScanModesSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmScanModesSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf2472a14dbbe96338899781382c13924754b89e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358049"
---
# <a name="filmscanmodessupported-element"></a>FilmScanModesSupported 元素


所需**FilmScanModesSupported**元素包含电影胶片扫描选项支持的公开类型的列表。

<a name="usage"></a>用法
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>Film</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**FilmScanModesSupported**元素包含一个或多个[ **FilmScanModeValue** ](filmscanmodevalue.md)子元素。 每个**FilmScanModeValue**元素标识电影扫描选项支持的电影胶片公开类型。

## <a name="see-also"></a>请参阅


[**Film**](film.md)

[**FilmScanModeValue**](filmscanmodevalue.md)

 

 






