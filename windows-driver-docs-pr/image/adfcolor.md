---
title: ADFColor 元素
description: 必需的 ADFColor 元素包含自动文档送纸器 (ADF) 支持的颜色处理功能的列表。
keywords:
- ADFColor 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a60cc89e72c140bb9c80d802c3af5ad0b2d7b8c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837767"
---
# <a name="adfcolor-element"></a>ADFColor 元素


必需的 **ADFColor** 元素包含自动文档送纸器 (ADF) 支持的颜色处理功能的列表。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFColor>
  child elements
</wscn:ADFColor>
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
<td><p><a href="colorentry.md" data-raw-source="[&lt;strong&gt;ColorEntry&lt;/strong&gt;](colorentry.md)"><strong>ColorEntry</strong></a></p></td>
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

**ADFColor** 元素包含确定扫描仪 ADF 支持的颜色处理和购置类型所需的信息。 如果父元素为 [**ADFFront**](adffront.md)，则指定的颜色信息适用于 ADF 的正面;否则，父元素为 [**ADFBack**](adfback.md) ，颜色信息适用于 ADF 的背面。

描述每个像素所需的信息量取决于特定的 [**ColorEntry**](colorentry.md) 关键字。 黑白图像需要每个像素 (bpp) ，而灰度和彩色图像需要更多的信息。 确切的信息量由扫描设备的颜色空间和技术功能决定。

返回的扫描数据的另一个重要方面是获取的数据的 photometric 解释。 扫描设备返回的所有图像数据都需要在白色显示黑色，其中黑色表示为0，白色表示为1。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**ColorEntry**](colorentry.md)

 

 






