---
title: ADFResolutions 元素
description: 必需的 ADFResolutions 元素包含一个分辨率列表，在该列表中，扫描仪的自动文档送纸器的前端或背面 (ADF) 可以扫描。
keywords:
- ADFResolutions 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94d66e150812567b3ae3961acee01199d85e643c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841117"
---
# <a name="adfresolutions-element"></a>ADFResolutions 元素


必需的 **ADFResolutions** 元素包含一个分辨率列表，在该列表中，扫描仪的自动文档送纸器的前端或背面 (ADF) 可以扫描。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFResolutions>
  child elements
</wscn:ADFResolutions>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

分辨率指定为 [**宽度**](width.md) x [**高度**](height.md) 对，其中的 **宽度** 和 **高度** 均以每英寸像素数来指定。

如果 **ADFResolutions** 元素的父元素为 [**ADFFront**](adffront.md)，则指定的分辨率适用于 ADF 的正面;否则，父元素为 [**ADFBack**](adfback.md) ，分辨率适用于 ADF 的背面。

WSD 扫描服务应列出扫描设备支持的 **宽度** 子元素中的所有可能宽度，以及扫描设备支持的 **高度** 子元素中的所有可能的高度。 所有的 **宽度** 和 **高度** 值都彼此独立，并且大多数设备将支持在 [**ScanTicket**](scanticket.md) 元素内的任何组合中配对它们。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**高度**](height.md)

[**Heights**](heights.md)

[**ScanTicket**](scanticket.md)

[**宽度**](width.md)

[**Widths**](widths.md)

 

 






