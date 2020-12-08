---
title: PlatenResolutions 元素
description: 必需的 PlatenResolutions 元素包含扫描仪的影印可扫描的分辨率列表。
keywords:
- PlatenResolutions 元素图像设备
topic_type:
- apiref
api_name:
- wscn PlatenResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 711b8c6b80c098d2f69f90b1c39d86b24617d282
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841073"
---
# <a name="platenresolutions-element"></a>PlatenResolutions 元素


必需的 **PlatenResolutions** 元素包含扫描仪的影印可扫描的分辨率列表。

<a name="usage"></a>使用情况
-----

```xml
<wscn:PlatenResolutions>
  child elements
</wscn:PlatenResolutions>
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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>Heights</strong></a></p></td>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>Platen</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

分辨率指定为 [**宽度**](width.md) x [**高度**](height.md) 对，其中的宽度和高度均以每英寸像素数来指定。

WSD 扫描服务应列出扫描设备支持的宽度子元素中的所有可能宽度，以及扫描设备支持的高度子元素中的所有可能的高度。 所有的宽度和高度值都彼此独立，并且大多数设备将支持在 [**ScanTicket**](scanticket.md) 元素内的任何组合中配对它们。

## <a name="see-also"></a>请参阅


[**高度**](height.md)

[**Heights**](heights.md)

[**Platen**](platen.md)

[**ScanTicket**](scanticket.md)

[**宽度**](width.md)

[**Widths**](widths.md)

 

 






