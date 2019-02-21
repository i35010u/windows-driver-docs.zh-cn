---
title: ADFResolutions 元素
description: 所需的 ADFResolutions 元素包含一系列的扫描程序的自动文档送纸器 (ADF) 的前端或后端可以扫描的解决方法。
ms.assetid: 6747b4d9-3333-4f06-9c1e-043dde24273c
keywords:
- ADFResolutions 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe90400bf7ce104e2b574f9404b102ac119acad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534263"
---
# <a name="adfresolutions-element"></a>ADFResolutions 元素


所需**ADFResolutions**元素包含一系列的扫描程序的自动文档送纸器 (ADF) 的前端或后端可以扫描的解决方法。

<a name="usage"></a>用法
-----

```xml
<wscn:ADFResolutions>
  child elements
</wscn:ADFResolutions>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

解决方法指定为[**宽度**](width.md) x [**高度**](height.md)对，其中同时**宽度**和**高度**以每英寸点数的像素为单位指定。

如果父元素的**ADFResolutions**元素是[ **ADFFront**](adffront.md)，指定的解决方法适用于 ADF 的正面; 否则，为父元素[ **ADFBack** ](adfback.md)和解决方法适用于 ADF 的后端。

WSD 扫描服务应列出扫描设备支持中的所有可能的宽度**宽度**子元素和扫描设备支持中的所有可能高度**高度**子元素。 所有**宽度**并**高度**的值为独立于彼此，和大多数设备将支持这些配对中的任意组合[ **ScanTicket**](scanticket.md)元素。

## <a name="see-also"></a>另请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**高度**](heights.md)

[**ScanTicket**](scanticket.md)

[**Width**](width.md)

[**Widths**](widths.md)

 

 






