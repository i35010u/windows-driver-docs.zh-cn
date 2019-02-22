---
title: FilmMaximumSize 元素
description: 所需的 FilmMaximumSize 元素指定最大大小原始的最终用户可以使用扫描输入的源电影扫描。
ms.assetid: 936c3c4e-5b09-433e-876c-9eda438dde9c
keywords:
- FilmMaximumSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4143b4b16c12c56bd6ded7a75bf2fa98248886c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556006"
---
# <a name="filmmaximumsize-element"></a>FilmMaximumSize 元素


所需**FilmMaximumSize**元素指定最大大小原始的最终用户可以使用扫描输入的源电影扫描。

<a name="usage"></a>用法
-----

```xml
<wscn:FilmMaximumSize>
  child elements
</wscn:FilmMaximumSize>
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

[**宽度**](width.md)子元素指定扫描输入的源电影支持快速扫描方向中的媒体的最大大小。 [**高度**](height.md)子元素指定扫描输入的源电影进行慢扫描方向中支持的媒体的最大大小。

所有媒体维度都以一个千分之几秒 (1/1000) 的英寸为单位。 两个可能的值**宽度**并**高度**范围从 1 到 2147483648。

## <a name="see-also"></a>另请参阅


[**Film**](film.md)

[**Height**](height.md)

[**Width**](width.md)

 

 






