---
title: PlatenMinimumSize 元素
description: 必需的 PlatenMinimumSize 元素指定最终用户可以在平板影印上扫描的最小大小的文档。
keywords:
- PlatenMinimumSize 元素图像设备
topic_type:
- apiref
api_name:
- wscn PlatenMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187aa3120e820ffd1cf49bb6d10468f159af29b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841077"
---
# <a name="platenminimumsize-element"></a>PlatenMinimumSize 元素


必需的 **PlatenMinimumSize** 元素指定最终用户可以在平板影印上扫描的最小大小的文档。

<a name="usage"></a>使用情况
-----

```xml
<wscn:PlatenMinimumSize>
  child elements
</wscn:PlatenMinimumSize>
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

[**Width**](width.md)子元素指定了在快速扫描方向上，影印支持的媒体的最小大小。 [**Height**](height.md)子元素指定在慢速扫描方向上，影印支持的介质的最小大小。

所有介质尺寸都按1分之 (1/1000) 英寸度量。 **宽度** 和 **高度** 的可能值范围是从1到2147483648。

## <a name="see-also"></a>请参阅


[**高度**](height.md)

[**Platen**](platen.md)

[**宽度**](width.md)

 

 






