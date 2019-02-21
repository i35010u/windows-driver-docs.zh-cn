---
title: PlatenMinimumSize 元素
description: 所需的 PlatenMinimumSize 元素指定的最小大小的文档的最终用户可以扫描平板辊上。
ms.assetid: 8db5092f-415c-4942-a4a7-733a381afd16
keywords:
- PlatenMinimumSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn PlatenMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64120f6376fecb2cb864e41b6c0a901f00e56d88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547208"
---
# <a name="platenminimumsize-element"></a>PlatenMinimumSize 元素


所需**PlatenMinimumSize**元素指定最小大小的文档的最终用户可以扫描平板辊上。

<a name="usage"></a>用法
-----

```xml
<wscn:PlatenMinimumSize>
  child elements
</wscn:PlatenMinimumSize>
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

[**宽度**](width.md)子元素指定辊支持快速扫描方向中的媒体的最小大小。 [**高度**](height.md)子元素指定辊支持进行慢扫描方向中的媒体的最小大小。

所有媒体维度都以一个千分之几秒 (1/1000) 的英寸为单位。 两个可能的值**宽度**并**高度**范围从 1 到 2147483648。

## <a name="see-also"></a>另请参阅


[**Height**](height.md)

[**辊**](platen.md)

[**Width**](width.md)

 

 






