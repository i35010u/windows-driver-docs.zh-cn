---
title: FilmMaximumSize 元素
description: 必需的 FilmMaximumSize 元素指定最终用户可使用胶片扫描输入源扫描的最大原始大小。
keywords:
- FilmMaximumSize 元素图像设备
topic_type:
- apiref
api_name:
- wscn FilmMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464daeb795e2d15226487e8f457ac131156f5d02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818937"
---
# <a name="filmmaximumsize-element"></a>FilmMaximumSize 元素


必需的 **FilmMaximumSize** 元素指定最终用户可使用胶片扫描输入源扫描的最大原始大小。

<a name="usage"></a>使用情况
-----

```xml
<wscn:FilmMaximumSize>
  child elements
</wscn:FilmMaximumSize>
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>高度</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>宽度</strong></a></p></td>
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

[**Width**](width.md)子元素指定电影扫描输入源在快速扫描方向上支持的最大介质大小。 [**Height**](height.md)子元素指定在慢速扫描方向上，胶卷扫描输入源支持的媒体的最大大小。

所有介质尺寸都按1分之 (1/1000) 英寸度量。 **宽度** 和 **高度** 的可能值范围是从1到2147483648。

## <a name="see-also"></a>请参阅


[**胶片**](film.md)

[**高度**](height.md)

[**宽度**](width.md)

 

 






