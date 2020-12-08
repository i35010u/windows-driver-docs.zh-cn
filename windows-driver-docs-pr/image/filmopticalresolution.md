---
title: FilmOpticalResolution 元素
description: 必需的 FilmOpticalResolution 元素指定电影扫描输入源可以扫描的最大光学分辨率。
keywords:
- FilmOpticalResolution 元素图像设备
topic_type:
- apiref
api_name:
- wscn FilmOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba3b400a865d6d880544ebccded1251465532ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801747"
---
# <a name="filmopticalresolution-element"></a>FilmOpticalResolution 元素


必需的 **FilmOpticalResolution** 元素指定电影扫描输入源可以扫描的最大光学分辨率。

<a name="usage"></a>使用情况
-----

```xml
<wscn:FilmOpticalResolution/>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


没有任何子元素。

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

如果没有 **高度** ，则 WSD 扫描服务应采用方形图像解析。 例如，如果仅提供 **Width** 元素100，则假定分辨率为 100 x 100 像素/平方英寸。

## <a name="see-also"></a>请参阅


[**胶片**](film.md)

[**高度**](height.md)

[**宽度**](width.md)

 

 






