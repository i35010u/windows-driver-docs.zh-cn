---
title: PlatenOpticalResolution 元素
description: 所需的 PlatenOpticalResolution 元素指定从该处辊可以扫描的最大光学分辨率。
ms.assetid: 770c204c-9315-47c6-afd3-4ac385e1177e
keywords:
- PlatenOpticalResolution 元素成像设备
topic_type:
- apiref
api_name:
- wscn PlatenOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe36297aa7e51605ec22e051d1af84dd00d0e7ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546050"
---
# <a name="platenopticalresolution-element"></a>PlatenOpticalResolution 元素


所需**PlatenOpticalResolution**元素指定从该处辊可以扫描的最大光学分辨率。

<a name="usage"></a>用法
-----

```xml
<wscn:PlatenOpticalResolution>
  child elements
</wscn:PlatenOpticalResolution>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>辊</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

解决方法指定为[**宽度**](width.md) x [**高度**](height.md)对，其中同时**宽度**和**高度**以每英寸点数的像素为单位指定。

如果未指定高度元素，WSD 扫描服务应假定正方形的图像分辨率。 例如，如果唯一**宽度**提供 100 个元素，假定解决方法是每平方英寸的 100 x 100 像素。

## <a name="see-also"></a>另请参阅


[**Height**](height.md)

[**辊**](platen.md)

[**Width**](width.md)

 

 






