---
title: 高度元素
description: 所需的高度元素包含具有高度扫描程序扫描图像的列表。
ms.assetid: b45a967e-9ce9-417a-96f2-c199ab302b88
keywords:
- 高度元素成像设备
topic_type:
- apiref
api_name:
- wscn Heights
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70b7ad6b8a7e165a71a3e70dfc041afb756ba676
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330274"
---
# <a name="heights-element"></a>高度元素


所需**高度**元素包含具有高度扫描程序扫描图像的列表。

<a name="usage"></a>用法
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>Height</strong></a></p></td>
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

每个[**高度**](height.md)子元素指定为有效的每英寸点数设备扫描图像的垂直像素数。

[**宽度**](widths.md)元素包含在扫描仪支持的宽度的列表。

## <a name="see-also"></a>请参阅


[**ADFResolutions**](adfresolutions.md)

[**FilmResolutions**](filmresolutions.md)

[**Height**](height.md)

[**PlatenResolutions**](platenresolutions.md)

[**Width**](width.md)

[**Widths**](widths.md)

 

 






