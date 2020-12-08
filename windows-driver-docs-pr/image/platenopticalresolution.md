---
title: PlatenOpticalResolution 元素
description: 必需的 PlatenOpticalResolution 元素指定影印可扫描的最大光学分辨率。
keywords:
- PlatenOpticalResolution 元素图像设备
topic_type:
- apiref
api_name:
- wscn PlatenOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b04033aaa60682abf161329df4a6d2271dc946e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841075"
---
# <a name="platenopticalresolution-element"></a>PlatenOpticalResolution 元素


必需的 **PlatenOpticalResolution** 元素指定影印可扫描的最大光学分辨率。

<a name="usage"></a>使用情况
-----

```xml
<wscn:PlatenOpticalResolution>
  child elements
</wscn:PlatenOpticalResolution>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>Platen</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

分辨率指定为 [**宽度**](width.md) x [**高度**](height.md) 对，其中的 **宽度** 和 **高度** 均以每英寸像素数来指定。

如果未指定 Height 元素，则 WSD 扫描服务应采用方形图像解析。 例如，如果仅提供 **Width** 元素100，则假定分辨率为 100 x 100 像素/平方英寸。

## <a name="see-also"></a>请参阅


[**高度**](height.md)

[**Platen**](platen.md)

[**宽度**](width.md)

 

 






