---
title: ADFMinimumSize 元素
description: 所需的 ADFMinimumSize 元素指定的最终用户可以扫描的最小大小原始前面或背面自动文档送纸器 (ADF)。
ms.assetid: 9304bb42-8ec4-4e79-95ce-af2aed4a58e2
keywords:
- ADFMinimumSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41758405f7a3c813a33f504762760424f7bc918
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555492"
---
# <a name="adfminimumsize-element"></a>ADFMinimumSize 元素


所需**ADFMinimumSize**元素指定最终用户可以扫描的最小大小原始前面或背面自动文档送纸器 (ADF)。

<a name="usage"></a>用法
-----

```xml
<wscn:ADFMinimumSize>
  child elements
</wscn:ADFMinimumSize>
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

[**宽度**](width.md)子元素指定 ADF 支持快速扫描方向中的媒体的最小大小。 [**高度**](height.md)子元素指定 ADF 支持进行慢扫描方向中的媒体的最小大小。

如果父元素的**ADFMinimumSize**元素是[ **ADFFront**](adffront.md)，指定的大小适用于 ADF 的正面; 否则，父元素是[**ADFBack** ](adfback.md)和大小适用于 ADF 的后端。

所有媒体维度都以一个千分之几秒 (1/1000) 的英寸为单位。 两个可能的值**宽度**并**高度**范围从 1 到 2147483648。

## <a name="see-also"></a>另请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**Width**](width.md)

 

 






