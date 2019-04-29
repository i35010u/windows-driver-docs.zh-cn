---
title: FilmColor 元素
description: 所需的 FilmColor 元素包含处理电影扫描输入的源支持的功能的颜色的列表。
ms.assetid: daea2cb8-a29f-4be8-bc58-8ed45d64870c
keywords:
- FilmColor 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4eda96116c285245e6884ae7dbeab9c4e9aee1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323257"
---
# <a name="filmcolor-element"></a>FilmColor 元素


所需**FilmColor**元素包含处理电影扫描输入的源支持的功能的颜色的列表。

<a name="usage"></a>用法
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>Film</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**FilmColor**元素包含确定色处理和获取扫描程序的电影胶片扫描输入的源支持的类型所需的信息。

描述每个像素所需的信息的量取决于特定于[ **ColorEntry** ](colorentry.md)关键字。 黑色和白色映像需要仅有一位每像素 (bpp)，而灰度和彩色图像需要更多的信息。 通过颜色空间并扫描设备的技术功能确定确切的信息量。

返回的扫描数据的另一个重要方面是测光获得的数据的解释。 需要为黑白色，其中 0 表示黑色和白色表示按 1 扫描设备返回的所有图像数据都。

## <a name="see-also"></a>请参阅


[**ColorEntry**](colorentry.md)

[**Film**](film.md)

 

 






