---
title: ADFMaximumSize 元素
description: 所需的 ADFMaximumSize 元素指定自动文档送纸器 (ADF) 的前端或后端上的最终用户可以扫描的大小最大的文档。
ms.assetid: 8304bbae-e0ed-40f3-b3aa-2a818664b76a
keywords:
- ADFMaximumSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8658597ae5544635a8515c68b9398d61f516ef86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520846"
---
# <a name="adfmaximumsize-element"></a>ADFMaximumSize 元素


所需**ADFMaximumSize**元素自动文档送纸器 (ADF) 的前端或后端上指定最大大小的文档的最终用户可以扫描。

<a name="usage"></a>用法
-----

```xml
<wscn:ADFMaximumSize>
  child elements
</wscn:ADFMaximumSize>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**宽度**](width.md)子元素指定 ADF 支持快速扫描方向中的媒体的最大大小。 [**高度**](height.md)子元素指定 ADF 支持进行慢扫描方向中的媒体的最大大小。

如果父元素的**ADFMaximumSize**元素是[ **ADFFront**](adffront.md)，指定最大大小适用于 ADF 的正面; 否则，为父元素[ **ADFBack** ](adfback.md)和最大大小适用于 ADF 的后端。

所有媒体维度都以一个千分之几秒 (1/1000) 的英寸为单位。 两个可能的值**宽度**并**高度**范围从 1 到 2147483648。

## <a name="see-also"></a>另请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**Width**](width.md)

 

 






