---
title: FilmColor 元素
description: 必需的 FilmColor 元素包含胶片扫描输入源支持的颜色处理功能的列表。
keywords:
- FilmColor 元素图像设备
topic_type:
- apiref
api_name:
- wscn FilmColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 551ef8e7e6cbcb0541c92cdd0970abcd48134204
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818941"
---
# <a name="filmcolor-element"></a>FilmColor 元素


必需的 **FilmColor** 元素包含胶片扫描输入源支持的颜色处理功能的列表。

<a name="usage"></a>使用情况
-----

```xml
<wscn:FilmColor>
  child elements
</wscn:FilmColor>
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
<td><p><a href="colorentry.md" data-raw-source="[&lt;strong&gt;ColorEntry&lt;/strong&gt;](colorentry.md)"><strong>ColorEntry</strong></a></p></td>
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

**FilmColor** 元素包含确定扫描仪的电影扫描输入源支持的颜色处理和获取类型所需的信息。

描述每个像素所需的信息量取决于特定的 [**ColorEntry**](colorentry.md) 关键字。 黑白图像需要每个像素 (bpp) ，而灰度和彩色图像需要更多的信息。 确切的信息量由扫描设备的颜色空间和技术功能决定。

返回的扫描数据的另一个重要方面是获取的数据的 photometric 解释。 扫描设备返回的所有图像数据都需要在白色显示黑色，其中黑色表示为0，白色表示为1。

## <a name="see-also"></a>请参阅


[**ColorEntry**](colorentry.md)

[**胶片**](film.md)

 

 






