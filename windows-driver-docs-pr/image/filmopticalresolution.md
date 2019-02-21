---
title: FilmOpticalResolution 元素
description: 所需的 FilmOpticalResolution 元素指定从该处可以扫描电影扫描输入的源的最大光学分辨率。
ms.assetid: 85e3b737-d5b0-4262-ab86-32b6aaf56e26
keywords:
- FilmOpticalResolution 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f67dde69cd576ac54057594eb2d3fbb6683513
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522287"
---
# <a name="filmopticalresolution-element"></a>FilmOpticalResolution 元素


所需**FilmOpticalResolution**元素指定从该处可以扫描电影扫描输入的源的最大光学分辨率。

<a name="usage"></a>用法
-----

```xml
<wscn:FilmOpticalResolution/>
```

<a name="attributes"></a>属性
----------

没有特性。

## <a name="child-elements"></a>子元素


没有子元素。

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

如果**高度**不存在，WSD 扫描服务应假定正方形的图像分辨率。 例如，如果唯一**宽度**提供 100 个元素，假定的解决方法是每平方英寸的 100 x 100 像素。

## <a name="see-also"></a>另请参阅


[**Film**](film.md)

[**Height**](height.md)

[**Width**](width.md)

 

 






