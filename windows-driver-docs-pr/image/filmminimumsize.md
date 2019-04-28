---
title: FilmMinimumSize 元素
description: 所需的 FilmMinimumSize 元素指定最小大小原始的最终用户可以使用扫描选项电影扫描。
ms.assetid: bce03ce1-9f2f-489f-ae71-a81474895410
keywords:
- FilmMinimumSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8251ec82e9558d267650015007ea6815393487ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354620"
---
# <a name="filmminimumsize-element"></a>FilmMinimumSize 元素


所需**FilmMinimumSize**元素指定最小大小原始的最终用户可以使用扫描选项电影扫描。

<a name="usage"></a>用法
-----

```xml
<wscn:FilmMinimumSize>
  child elements
</wscn:FilmMinimumSize>
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
<tr class="even">
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>Film</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**宽度**](width.md)子元素指定扫描输入的源电影支持快速扫描方向中的媒体的最小大小。 [**高度**](height.md)子元素指定扫描输入的源电影进行慢扫描方向中支持的媒体的最小大小。

所有媒体维度都以一个千分之几秒 (1/1000) 的英寸为单位。 两个可能的值**宽度**并**高度**范围从 1 到 2147483648。

## <a name="see-also"></a>请参阅


[**Film**](film.md)

[**Height**](height.md)

[**Width**](width.md)

 

 






