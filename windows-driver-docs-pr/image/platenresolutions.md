---
title: PlatenResolutions 元素
description: 所需的 PlatenResolutions 元素包含一系列的扫描程序的辊可以扫描的解决方法。
ms.assetid: 9adf54d7-4cca-4d43-b467-c0b2c84a4a7f
keywords:
- PlatenResolutions 元素成像设备
topic_type:
- apiref
api_name:
- wscn PlatenResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a70e40e26d8475d4b6631e6fb2e76dc2f44f45d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555746"
---
# <a name="platenresolutions-element"></a>PlatenResolutions 元素


所需**PlatenResolutions**元素包含一系列的扫描程序的辊可以扫描的解决方法。

<a name="usage"></a>用法
-----

```xml
<wscn:PlatenResolutions>
  child elements
</wscn:PlatenResolutions>
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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>高度</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="widths.md" data-raw-source="[&lt;strong&gt;Widths&lt;/strong&gt;](widths.md)"><strong>Widths</strong></a></p></td>
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

解决方法指定为[**宽度**](width.md) x [**高度**](height.md)对，其中以每英寸点数的像素为单位指定宽度和高度。

扫描设备支持宽度子元素内的所有可能的宽度和高度子元素内支持扫描设备的所有可能高度应列出 WSD 扫描服务。 所有的宽度和高度值都是独立于彼此，和大多数设备将支持这些配对中的任意组合[ **ScanTicket** ](scanticket.md)元素。

## <a name="see-also"></a>另请参阅


[**Height**](height.md)

[**高度**](heights.md)

[**辊**](platen.md)

[**ScanTicket**](scanticket.md)

[**Width**](width.md)

[**Widths**](widths.md)

 

 






